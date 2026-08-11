# Security

We take the security of Tagaris seriously. This page explains how to report a
problem and how the product is set up to keep your data safe.

## Reporting a vulnerability

If you find a security issue, please email security@goodhallsolutions.co.uk. Do not
open a public issue for it.

Tell us what you found, how to reproduce it, and the impact you think it has. We
aim to acknowledge a report within 3 working days and to keep you updated
while we work on a fix. Please give us reasonable time to fix an issue before
sharing it publicly.

## How Tagaris is built for security

- **Self-hosted, no phone home.** The app runs on your infrastructure. It verifies
  its licence offline and does not send your asset data to us.
- **Access control.** Roles (SuperAdmin, Admin, Editor, Viewer) are enforced by a
  central least-privilege check on the server, not just hidden in the UI.
- **Authentication.** Email and password with optional two-factor (an
  authenticator app, an email code, or backup codes), and optional Microsoft Entra
  single sign-on with a "require single sign-on" policy. The auth endpoints are
  rate limited to slow brute force.
- **Secrets at rest.** Integration and mail credentials are encrypted with
  AES-256-GCM, keyed from the install secret.
- **Your data is portable.** Full CSV and JSON export is always available, so you
  are never locked in.

## Running it safely

- Set a strong, unique `BETTER_AUTH_SECRET`.
- Serve the app over HTTPS, behind a reverse proxy that terminates TLS. Set
  `BETTER_AUTH_URL` to the exact public URL.
- Keep the container image up to date, and take regular database and photo
  backups (see [the install guide](https://docs.tagaris.co.uk/self-hosting) and
  [Backups and restore](https://docs.tagaris.co.uk/backups)).
- Restrict who can reach the database. It is not exposed outside the Compose
  network by default.

## Images and dependencies

Release images are built for linux/amd64 and linux/arm64 with provenance and
SBOM attestations, and scanned with Docker Scout. We track dependency
advisories and update on a regular cadence.
