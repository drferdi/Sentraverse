# Operations Runbook — Sentraverse

This runbook describes only what the repository states. It does not authorize
production intervention. For release authority and gates, see `docs/RELEASES.md`.

## Commands (capsule root, via `node scripts/pnpm.mjs` — `AGENTS.md`)

| Purpose | Command |
| --- | --- |
| Install | `node scripts/pnpm.mjs install --frozen-lockfile` |
| Lint | `node scripts/pnpm.mjs run lint` (`eslint .`) |
| Typecheck | `node scripts/pnpm.mjs run typecheck` (`tsc --noEmit`) |
| Test | `node scripts/pnpm.mjs run test` (`node --test app/api/medical-knowledge/route.test.mjs`) |
| Build | `node scripts/pnpm.mjs run build` (`next build --webpack`) |
| Run | `node scripts/pnpm.mjs run start` (serves `127.0.0.1:4340`; contract smoke: `GET /` → 200) |
| Deploy dry-run | `node scripts/pnpm.mjs run deploy:dry-run` |
| Browser E2E smoke | `node scripts/pnpm.mjs run test:e2e` (`playwright test` over `e2e/smoke.spec.ts`; needs Playwright browsers installed) |

Local development: `pnpm dev` (webpack, stable) or `pnpm dev:turbo` (experimental) on
`http://localhost:3000`; production preview via `pnpm build && pnpm start`
(`README.md` §17, `docs/setup.md`). Use pnpm, not npm/yarn/bun (`README.md` §17).
The site runs with zero required environment configuration (`README.md` §17).

## Configuration and secrets posture

- Optional env vars (`README.md` §18, `project.contract.json`, `next.config.mjs`):
  `NEXT_PUBLIC_PILOT_LOGIN_URL` (client CTA target; allow-listed to `sentrahai.com`
  hosts, falls back to `/dashboard`), `SENTRA_DASHBOARD_URL` (server; enables
  `/dashboard/:path*` rewrites), `SENTRA_ASSISTVERSE_URL` (server; `/asisten-medis`
  rewrite, defaults to `https://site-assist-seven.vercel.app`), `GEMINI_API_KEY`
  (optional; `/api/medical-knowledge` forwards the question only when set —
  `docs/data.md`, nothing persisted).
- `.env.example` lists placeholder entries (`NEXTAUTH_SECRET`, `NEXTAUTH_URL`,
  `DATABASE_URL`, `ANTHROPIC_API_KEY`, `SENTRY_DSN` as `TO_BE_SUPPLIED_BY:*`); the repo
  states no env vars are required to run the dev server (`docs/setup.md`).
- Never expose secrets or patient data; do not use production credentials or production
  data (`AGENTS.md`). Name environment variables, never their values (`.agents/CONTEXT.md`
  convention). No hardcoded secrets, API keys, or credentials in PRs (PR template
  security checklist).

## Deployment targets (as documented — verify before operating)

- `docs/deployment.md` documents Railway (auto-detected Next.js; `npm run build` /
  `npm run start`; production `https://sentrahai.com`; rollback via `railway rollback`
  or dashboard redeploy; post-deploy `curl` checks for headers, sitemap, robots,
  `llms.txt`).
- `.agents/HANDOFF.md` (2026-09-26) records the next action as re-pointing the Vercel
  project for `sentrahai.com` to the capsule root (Chief); `.github/workflows/ci.yml`
  header notes "Deploy ditangani Vercel".
- Current production target: belum dikonfirmasi / not yet confirmed. Two conflicting
  sources exist: `docs/deployment.md` documents Railway (auto-detected Next.js;
  `npm run build` / `npm run start`; production `https://sentrahai.com`; rollback via
  `railway rollback` or dashboard redeploy), while `.agents/HANDOFF.md` (2026-09-26)
  records the next action as re-pointing the Vercel project for `sentrahai.com` to the
  capsule root (Chief) and the `.github/workflows/ci.yml` header notes "Deploy
  ditangani Vercel". Do not operate on either assumption until the owner confirms.

## Health signals and verification

- Contract smoke: `GET http://127.0.0.1:4340/` → `200`, artifact `.next/BUILD_ID`
  (`project.contract.json`).
- Deploy dry-run (`scripts/deploy-dry-run.mjs`, no network, no credentials): requires
  `.next/BUILD_ID` (build first) and fails if `GEMINI_API_KEY` or
  `SENTRA_DASHBOARD_URL` appear in the client bundle.
- E2E smoke (`e2e/smoke.spec.ts`): homepage `main` landmark renders; `/insights`,
  `/story`, `/privacy`, `/terms` return 200; `#contact` with "Join Waiting List" link is
  visible. `playwright.config.ts` serves `pnpm dev` with 120s timeout.
- Security headers on all routes (`next.config.mjs` `headers()`, `SECURITY.md`):
  `X-Content-Type-Options`, `X-Frame-Options: DENY`, `X-XSS-Protection`,
  `Referrer-Policy`, `Permissions-Policy`, `Strict-Transport-Security`
  (`max-age=63072000; includeSubDomains; preload`), `Content-Security-Policy`.
- Manual checklist before production (`docs/testing.md`): 15 home components without
  console errors, nav/overlay behavior, article pages + 404 for unknown slugs, SEO nodes
  (JSON-LD, sitemap, robots, `llms.txt`), responsive breakpoints, header presence via
  `curl -I`.

## Incident handling

- Report vulnerabilities privately per `SECURITY.md` (see `docs/OWNERSHIP.md`); do not
  open a public issue.
- Preserve evidence, restrict sensitive data, and request authorization before any
  production intervention. This site processes no PHI and has no database or user
  sessions (`SECURITY.md`, `docs/data.md`).

Monitoring, alert routing, on-call ownership, backup/restore scope (static site —
whether any state needs recovery), and capacity/cost ownership: Belum dikonfirmasi.
No runbook in the repo states these today; do not infer them from this file.
