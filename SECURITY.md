# Security and privacy notes

This project is a static browser application. It does not provide authentication, a server-side audit log, encrypted record storage, role-based permissions, or a clinical data backend.

Before entering protected health information, deploy it only within controls approved by the clinic. Consider access restriction at the Cloudflare layer, managed clinic devices, automatic browser-data clearing, and a private GitHub repository.

Do not commit real patient information, completed forms, screenshots containing patient data, browser storage exports, credentials, access tokens, or environment files to this repository.

## Headers and CSP

`public/_headers` sets a restrictive CSP (`default-src 'self'`, no framing, no third-party origins), HSTS, and locked-down `Permissions-Policy`. `script-src`/`style-src` still allow `'unsafe-inline'` because the app ships as a single static HTML file with an inline `<script>`/`<style>` and there is no server available to issue per-response nonces on Cloudflare Pages. A hash-based CSP was considered but rejected: it would need to be recomputed on every edit to `public/index.html`, and a stale hash silently breaks the entire app for end users. Keep this in mind before adding any third-party script, iframe, or remote font — the current CSP will block them by default, which is intentional.

## Referral database accuracy

Resource entries carry a `verificationStatus` (web-reviewed vs. staff-verified) and a `verificationRisk` tier, visible in the app's Database view and verification queue. "Official page reviewed" means the source was checked against a public/official page during this development pass — it is not the same as a staff member calling to confirm current availability, payer rules, and intake steps. Do not treat any entry as ready for patient handoff until staff verification is logged.
