# Security Policy

## Supported versions

Security fixes are made against the latest maintained version on the default branch. Older releases may not receive security updates; deploy the latest reviewed release and rebuild the production image after security fixes.

## Reporting a vulnerability

Please do not report suspected vulnerabilities in public issues. Use GitHub's **Report a vulnerability** action in the repository's **Security** tab to send a private advisory to the maintainers.

If private vulnerability reporting is unavailable, contact the repository owner through a verified private channel listed in the repository profile. Do not include exploit details in a public issue or pull request.

Include the affected commit or release, impact, reproduction steps, and any suggested mitigation. Allow the maintainers reasonable time to investigate and prepare a fix before public disclosure. Do not access or alter other people's data while validating a report.

## Deployment security

- Keep SMTP credentials, deployment secrets, and `.env` files out of Git, image layers, build arguments, logs, and browser bundles.
- Use protected runtime configuration and restrict VPS and repository access to trusted operators.
- Keep the app behind the self-hosted reverse proxy; expose only intended public ports.
- Keep dependencies and the production Node base image updated, then rebuild and redeploy reviewed fixes.
- Contact submissions contain personal information. Do not log full payloads or retain enquiry data beyond the configured mail delivery path without a documented business and privacy requirement.
- Do not send real customer data or production secrets in public bug reports.
