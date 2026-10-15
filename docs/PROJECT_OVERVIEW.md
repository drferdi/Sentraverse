> SPS_REVIEW_REQUIRED — this file is an unreviewed scaffold. A repository owner must verify every statement against the sources cited and remove this marker only after review.

# Project Overview — Sentraverse

Public Sentra marketing website and platform hub for `sentrahai.com` (see `AGENTS.md`
"Objective and ownership" and `.agents/CONTEXT.md`). Domain: `healthcare`
(`project.contract.json` id `healthcare/sentraverse`).

## What this repository is

- **Project:** Sentraverse — the official website, product narrative layer, and public
  knowledge surface for Sentra Healthcare AI (`README.md` §01).
- **Audience stated in `README.md`:** Puskesmas, klinik pratama, referral hospitals,
  clinicians, healthcare operators, public-sector stakeholders, and technical partners.
- **Clinical posture:** clinical decision support (CDSS). Sentra supports clinical
  reasoning, triage awareness, workflow acceleration, and timely escalation; it does not
  replace professional medical judgment (`README.md` §10–§11, §24; `docs/ai-governance.md`,
  `docs/clinical-logic.md`).
- **Human owner:** Chief (dr. Ferdi Iskandar) — `AGENTS.md`, `project.contract.json`
  (`owner`), `.agents/CONTEXT.md`.
- **Default risk:** `R1`. Breaking public routes or the `/dashboard` and `/asisten-medis`
  rewrites needs review (`AGENTS.md`).

## Product surfaces and routes

Content surfaces and routes as documented in `README.md` §07 and §12 (verified against
`app/`):

| Surface | Route | Source |
| --- | --- | --- |
| Clinical-AI landing (15-section scroll experience, `app/page.tsx`) | `/` | `app/page.tsx`, `README.md` §08–§09 |
| Founder story, milestones, roadmap | `/story` | `app/story/` |
| Clinical-AI editorial index (`app/insights/data.ts`) | `/insights`, `/insights/[slug]` | `app/insights/` |
| 144-disease primary-care clinical reference | `/sentrapedia` | `app/sentrapedia/`, `components/sentrapedia/` |
| Product ecosystem and application catalog | `/ekosistem` | `app/ekosistem/`, `components/ekosistem/` |
| Architecture, governance, compliance knowledge base | `/sentrawiki` | `app/sentrawiki/`, `components/sentrawiki/` |
| Privacy policy / Terms of use | `/privacy`, `/terms` | `app/privacy/`, `app/terms/` |
| Supporting API routes | `/api/medical-knowledge`, `/api/melinda/chat`, `/api/melinda/ocr`, `/api/sentra-assist` | `app/api/` |
| Dashboard rewrite (proxied when `SENTRA_DASHBOARD_URL` is set) | `/dashboard/:path*` | `next.config.mjs` `rewrites()` |
| Assistverse rewrite (defaults to `https://site-assist-seven.vercel.app`) | `/asisten-medis`, `/asisten-medis/:path*` | `next.config.mjs` `rewrites()` |

SEO/discoverability assets: `app/sitemap.ts`, `app/robots.ts` (disallows `/dashboard`),
`app/opengraph-image.tsx`, JSON-LD in `app/layout.tsx`, `public/llms.txt`, Google Search
Console file `app/google22238cc24e0d1002.html` (`README.md` §20, `CHANGELOG.md`).

## Non-goals and boundaries (from the repo)

- No database and no persistent data: content is static TypeScript data under `app/` and
  `components/`; no patient data is collected or stored (`docs/data.md`,
  `docs/data-model.md`, `docs/privacy.md`).
- No autonomous diagnosis or treatment claims; Sentra AI is not registered as a medical
  device (`README.md` §24, `LICENSE` "CLINICAL DISCLAIMER").
- Never expose secrets or patient data; do not use production credentials or production
  data (`AGENTS.md` "Prohibited actions").

## Stack (verified in `package.json`)

- Next.js `16.3.8` (App Router, `--webpack` for dev/build), React 19, TypeScript `5.9`
  (strict), Tailwind CSS v4 (`@theme` in `app/globals.css`), GSAP `3.14` + ScrollTrigger,
  Framer Motion `12`, `pnpm@11.21.0`.
- Runtime contract: Node 24 (`project.contract.json`, `.github/workflows/ci.yml`
  `node-version: '24'`); `package.json` `engines` requires `>=24 <25`. `README.md` §17
  states Node `>= 22` / pnpm `>= 9` — TODO for Gaffer: confirm which minimum the docs
  should state.
- Package name/version: `@the-abyss/sentraverse` `1.0.0` (`package.json`).
- Standalone capsule: own `pnpm-workspace.yaml`, lockfile, scripts, and build config; no
  dependency on an enclosing workspace (`AGENTS.md`, `pnpm-workspace.yaml` comments).

## Scripts (`package.json`, run via `node scripts/pnpm.mjs` per `AGENTS.md`)

| Script | Command |
| --- | --- |
| `dev` | `next dev --webpack` (local server `http://localhost:3000` per `README.md` §17) |
| `dev:turbo` | `next dev --turbopack` |
| `build` | `next build --webpack` |
| `start` | `next start --hostname 127.0.0.1 --port 4340` (contract `run`/smoke: `127.0.0.1:4340/`) |
| `lint` | `eslint .` |
| `typecheck` | `tsc --noEmit` |
| `test` | `node --test app/api/medical-knowledge/route.test.mjs` |
| `test:e2e` | `playwright test` (`e2e/smoke.spec.ts`; needs Playwright browsers installed) |
| `deploy:dry-run` | `node scripts/deploy-dry-run.mjs` (requires `.next/BUILD_ID`; fails if server-only names `GEMINI_API_KEY`, `SENTRA_DASHBOARD_URL` appear in the client bundle) |

External services are declared by environment-variable name only
(`project.contract.json`): npm registry (required), `GEMINI_API_KEY` (optional, for
`/api/medical-knowledge`), `SENTRA_DASHBOARD_URL` (optional), `SENTRA_ASSISTVERSE_URL`
(optional). Client CTA target `NEXT_PUBLIC_PILOT_LOGIN_URL` falls back to `/dashboard`
(`README.md` §18).

## Repository map (top level)

`AGENTS.md`, `ARCHITECTURE.md`, `CHANGELOG.md`, `CONTRIBUTING.md`, `SECURITY.md`,
`README.md`, `ROADMAP.md`, `LICENSE`, `app/`, `components/`, `lib/`, `src/` (README only),
`tests/` (README only), `docs/`, `e2e/`, `public/`, `scripts/` (`deploy-dry-run.mjs`,
`pnpm.mjs`, `setup.sh`), `next.config.mjs` (security headers + rewrites), `package.json`,
`pnpm-workspace.yaml`, `pnpm-lock.yaml`, `.github/` (CI `lint` + `build`, PR template),
`.agents/` (`HANDOFF.md`, `CONTEXT.md`, `DECISIONS.md`).

Canonical docs: `README.md`; `ARCHITECTURE.md` (deep-dive) with overview in
`docs/architecture.md`; `docs/` index in `docs/README.md`; `CHANGELOG.md` (Keep a
Changelog / SemVer); `CONTRIBUTING.md`; `SECURITY.md`.

## Contacts stated in the repo

- Founder & CEO: dr. Ferdi Iskandar (`README.md` §26).
- Email (public site contact): `drferdiiskandar@sentrahai.com` (`README.md` §26).
- License/security contact: `drferdiiskandar@melinda.co.id`, web `https://sentrahai.com`
  (`LICENSE`, `SECURITY.md` with `[SECURITY]` subject line).
- Lab/location as stated in `README.md` §26: Melinda Advanced Technology Laboratory,
  Kediri, East Java.

TODO for Gaffer: confirm the current public contact address and which inbox handles
security reports, licensing requests, and pilot inquiries.

## Success criteria (repo-stated)

- Production-facing changes pass build, lint, and Playwright smoke validation
  (`README.md` §17); CI runs `lint` then `build` on push/PR to `main`/`master`
  (`.github/workflows/ci.yml`).
- TypeScript strict build, ESLint, Playwright smoke, stable GSAP pinned sections,
  CDSS-boundary language, visible accurate medical disclaimer, valid sitemap/robots/
  metadata/OG/JSON-LD (`README.md` §19).
- Clinical claims (statistics, accuracy metrics, demo dataset values) require Chief
  sign-off before merge (`CONTRIBUTING.md`, `docs/ai-governance.md`, PR template).
