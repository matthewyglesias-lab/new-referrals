# Security and privacy notes

This project is a static browser application. It does not provide authentication, a server-side audit log, encrypted record storage, role-based permissions, or a clinical data backend.

Before entering protected health information, deploy it only within controls approved by the clinic. Consider access restriction at the Cloudflare layer, managed clinic devices, automatic browser-data clearing, and a private GitHub repository.

Do not commit real patient information, completed forms, screenshots containing patient data, browser storage exports, credentials, access tokens, or environment files to this repository.
