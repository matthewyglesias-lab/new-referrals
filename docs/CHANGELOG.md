# v70 Data Verification, Specialists, Testing Referrals, Easy Referrals

- Fact-checked all 131 existing resources (phone/address against each live sourceUrl, corroborated via search where a site blocked automated fetches) and fixed 2 real errors found: `lluh-murrieta-youth-php-iop` had the wrong phone number for the youth PHP/IOP line (was 951-290-6411, corrected to 951-783-3964), and `grow-through-life-ca`'s city label misleadingly implied a Riverside-city office that doesn't exist (corrected to "California online / Murrieta-Temecula").
- Added 2 individual eating-disorder outpatient specialists (distinct from the program-level PHP/IOP/residential entries added previously): Inland Empire Behavioral Group (Riverside/Colton -- individual therapy, medication management, nutrition support) and Nourished with Kindness (CA telehealth eating-disorder-specialized registered dietitians).
- Added 3 neuropsychological/ADHD testing resources to a previously thin "Testing DD" category: NeuroChamp (Riverside, psychoeducational/ADHD/learning/autism testing), Abundance Therapy Center (Riverside, ADHD testing ages 6+, ~2-3 week wait), and Nixon Psychological Institute (Chino, ages 3+, ADHD/cognitive/learning/autism testing).
- Added a new staff-facing "Easy online referrals" panel on the Database screen: resources with a real, verified external-provider referral-submission portal (not just a patient self-assessment link) now get a `referralSubmitUrl` field and a direct "Submit referral online" button. Verified and wired up Octave, Talkiatry, and Brightside Health's genuine clinician referral forms (SonderMind's clinician referral was checked and excluded -- SonderMind doesn't currently serve California).
- Resource count: 131 → 136.

# v69 Eating Disorder Referrals + Repo Hardening

- Reconstructed the repository into the documented `public/`, `docs/`, and `.github/workflows/` layout; the prior commit had every file's name mismatched with its content (a scrambled zip extraction), so nothing in the repo actually matched the deployable v68 package.
- Recreated `public/favicon.svg`, `public/manifest.webmanifest`, and `public/robots.txt`, whose original content was missing entirely from the scrambled commit.
- Added 7 verified eating-disorder referral resources to close the "Eating disorder treatment" coverage gap flagged in the database's own verification queue: San Bernardino County's Eating Disorder Collaborative, Riverside University Health System's Mindful Body and Recovery Program (Medi-Cal ED-IOP), Bright Road Recovery (Claremont, residential/PHP/IOP), Eating Recovery Center Irvine (PHP/IOP), ACUTE Center for Eating Disorders & Severe Malnutrition (medical-stability exclusion route), and two virtual options (Equip for family-based treatment, Within Health for virtual PHP/IOP). Resource count: 124 → 131.
- Added a `Strict-Transport-Security` header and fixed a CI bug where the "reject accidental secrets" check matched its own pattern text and would fail on every run.
- Added a CI step that parses every inline `<script>` block with `node --check` so a future hand-edit of the single-file app can't silently break the build.

# v68 Cloudflare Static Release

- Packaged the app as a true Cloudflare Pages static deployment with `index.html` at the ZIP root.
- Added SPA routing, deployment security headers, no-index controls, favicon, and installable web-app metadata.
- Removed remaining overlay compositing and hover movement that could make drawers feel fuzzy or jittery.
- Standardized input, select, textarea, button, focus, checkbox, and dialog geometry.
- Added correct native autofill, capitalization, and mobile keyboards for patient, provider, staff, DOB, phone, fax, date, and page fields.
- Made the output rail and preview independently stable on large screens while preserving safe stacking on smaller screens.
- Fixed truncated output-builder badges and low-contrast selected-output text.
- Rechecked all 124 resource drawers and all seven generated outputs.
- Replaced residual internal payer terminology in drawer instructions and generated documents with clear insurance language.
