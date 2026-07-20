name: Validate static release

on:
  push:
    branches: [main]
  pull_request:

permissions:
  contents: read

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Validate required deployment files
        shell: bash
        run: |
          set -euo pipefail
          required=(
            public/index.html
            public/_headers
            public/_redirects
            public/favicon.svg
            public/manifest.webmanifest
            public/robots.txt
          )
          for file in "${required[@]}"; do
            test -s "$file" || { echo "Missing or empty: $file"; exit 1; }
          done

      - name: Validate application shell and routing
        shell: bash
        run: |
          set -euo pipefail
          grep -qi '<!doctype html' public/index.html
          grep -qi '<title' public/index.html
          grep -q '/\* /index.html 200' public/_redirects
          grep -q 'Content-Security-Policy:' public/_headers
          grep -q 'Disallow: /' public/robots.txt

      - name: Reject common accidental secrets
        shell: bash
        run: |
          set -euo pipefail
          if grep -RInE --exclude-dir=.git --exclude='*.md' \
            '(BEGIN (RSA|OPENSSH|EC|DSA) PRIVATE KEY|AWS_SECRET_ACCESS_KEY|CLOUDFLARE_API_TOKEN|GITHUB_TOKEN=)' .; then
            echo 'Possible secret detected.'
            exit 1
          fi
