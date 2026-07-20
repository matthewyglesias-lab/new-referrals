# IPMG Referral Hub

Behavioral-health referral planning and output workspace for Inland Psychiatric Medical Group staff.

This repository is arranged for **GitHub → Cloudflare Pages** deployment. The deployable site is isolated in `public/`; release notes and QA evidence remain in `docs/` and are not published with the application.

## Cloudflare Pages settings

Connect this repository in Cloudflare Pages and use:

| Setting | Value |
|---|---|
| Production branch | `main` |
| Framework preset | None |
| Build command | Leave blank |
| Build output directory | `public` |
| Root directory | `/` |

After the initial connection, each push to `main` creates a new production deployment. Pull-request branches can be used for preview deployments before merging.

## Repository layout

```text
public/                  Static application deployed by Cloudflare Pages
  index.html             Application entry point
  _headers               Security and cache headers
  _redirects             Single-page-app fallback
  favicon.svg
  manifest.webmanifest
  robots.txt

docs/                    Release notes, QA results, and package metadata
.github/workflows/        Lightweight repository validation
```

## Local preview

Any basic static server can serve the `public/` directory. For example, with Python installed:

```bash
python -m http.server 8080 --directory public
```

Then open `http://localhost:8080`.

## Data and access considerations

- The application is fully static and has no backend database.
- User-entered state is stored in the browser's local storage.
- The app itself does not transmit referral or patient data to a server.
- A Cloudflare Pages URL is not access-controlled by default. Use only clinic-approved access controls and device policies when real patient information may be entered.
- Avoid using shared browser profiles for patient-related work because local storage can remain on the device.

## Release

Current packaged release: **v68 Cloudflare Static Release**.

See [`docs/RELEASE_QA_REPORT.md`](docs/RELEASE_QA_REPORT.md) and [`docs/CHANGELOG.md`](docs/CHANGELOG.md).
