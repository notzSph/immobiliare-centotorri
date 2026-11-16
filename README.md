# Immobiliare Centotorri

[![Version](https://img.shields.io/badge/version-1.0.0-blue)](package.json)
![Frontend](https://img.shields.io/badge/frontend-Astro-BC52EE)
![Language](https://img.shields.io/badge/language-TypeScript-3178C6)
![Runtime](https://img.shields.io/badge/runtime-Node.js-339933)
![Deployment](https://img.shields.io/badge/deployment-Docker-2496ED)
[![Build](https://github.com/notzSph/immobiliare-centotorri/actions/workflows/ci.yml/badge.svg)](https://github.com/notzSph/immobiliare-centotorri/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

A lightweight Italian real estate website built with Astro and TypeScript, styled with the project's zkit/zspinach inspired SCSS utilities, and deployed in Docker on a privately managed VPS.

## Features

- Homepage, services, property portfolio, property detail pages, and contact page.
- Property and agency content stored in typed repository files.
- Prerendered pages with small progressive enhancements for navigation, filters, galleries, and contact form feedback.
- Self-hosted contact endpoint that delivers enquiries through an operator-managed SMTP relay.
- Docker deployment behind a self-hosted HTTPS reverse proxy.

## Requirements

- Node.js version supported by the pinned Astro and Node adapter dependencies.
- Docker Engine and Docker Compose for container validation and deployment.
- A private VPS, a configured domain, and an HTTPS reverse proxy for production.
- An operator-managed SMTP relay for contact enquiries.

## Local development

```sh
npm ci
npm run dev
```

The development server prints its local URL. Use the configured project scripts for checks and content validation:

```sh
npm run check
npm run validate:content
npm run test
npm run build
```

Scripts can vary while the project is being scaffolded. Check `package.json` for the commands currently available.

## Content updates

Agency details are maintained in `src/lib/data/agency.ts`. Services and page copy live in `src/lib/data/`. Each property has a typed record under `src/lib/data/properties/`, and its photographs belong under `src/assets/properties/<slug>/`.

Use verified facts only. Set a property's status explicitly, use `null` for price on request, and supply useful alt text for informative images. Run content validation and build the site after edits.

See [docs/content-editing.md](docs/content-editing.md) when available for the full editing guide, and [docs/architecture.md](docs/architecture.md) for the system design.

## Self-hosted deployment

The production image runs Astro's standalone Node server. The public pages are prerendered during the image build; `/api/contact` and `/healthz` run inside the container. Put the app behind the VPS reverse proxy and expose only the proxy to the internet.

1. Configure runtime secrets on the VPS using a protected environment file or secret files. Never commit real credentials.
2. Set the public site origin at build time for canonical URLs and sitemap generation.
3. Configure the operator-managed SMTP relay and fixed recipient/sender values.
4. Configure the domain and HTTPS at the self-hosted reverse proxy.
5. Build and start the Compose service using the deployment procedure in [docs/deployment.md](docs/deployment.md) when available.
6. Check `/healthz`, the primary pages, property routes, and contact form behaviour.

The app container is not a mail server. SMTP settings must refer to a relay reachable from inside the container; `localhost` inside a container refers to that container. Do not replace the relay with a hosted form or email API without an explicit architecture decision.

## Environment configuration

Copy `.env.example` to a protected deployment location and fill in the documented values. The example must contain placeholders only. Keep build-time public settings separate from runtime secrets. See [SECURITY.md](SECURITY.md) for vulnerability reports and secret handling.

## License

This project is distributed under the MIT License. See [LICENSE](LICENSE).