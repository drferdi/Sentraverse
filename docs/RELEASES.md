> SPS_REVIEW_REQUIRED — this file is an unreviewed scaffold. A repository owner must verify every statement against the sources cited and remove this marker only after review.

# Release Procedure — Sentraverse

This file documents the release mechanics the repository states. It does not authorize
any release, publish, merge, push, or deployment.

## Versioning and changelog

- Versioning: Semantic Versioning; changelog format: Keep a Changelog (`CHANGELOG.md`
  header). Current package version: `1.0.0` (`package.json` `version`).
- `[Unreleased]` section records the 2026-04-18 docs-truth audit and planned items
  (lazy-loading, per-page OG metadata, `ClinicalPrognosis` promotion, OpenTelemetry,
  RSC migration, bundle-analyzer wiring); `[1.0.0]` (2026-03-16) records pages, the four
  articles in `app/insights/data.ts`, landing sections, UI primitives, design tokens,
  SEO/metadata, and infrastructure (`CHANGELOG.md`).
- TODO for Gaffer: confirm who cuts a version (bumps `package.json`, writes
  `CHANGELOG.md`) and the tagging convention — the repo states the format but no release
  owner or tag practice.

## Authority and gates

- Clinical content gate: new clinical claims (statistics, accuracy metrics), article
  content, demo data in `SentraSim`/`ClinicalTrajectory`/`ClinicalPrognosis`, and
  `public/llms.txt` metric changes require Chief (Dr. Ferdi Iskandar) review
  (`CONTRIBUTING.md`, `docs/ai-governance.md`, PR template content checklist).
- Quality gate: `lint` with zero ESLint errors and `build` (strict TypeScript) with zero
  errors; CI enforces `lint` before `build` on push/PR (`.github/workflows/ci.yml`;
  pnpm `11.21.0`, Node `24`, `--frozen-lockfile`).
- Security gate (PR template): no hardcoded secrets; no new `next.config.mjs`
  `remotePatterns` domains without justification; no `headers()` changes without review.
- SEO gate (PR template + `README.md` §19): new routes in `app/sitemap.ts` with correct
  `changeFrequency`/`priority`, updated meta descriptions and OG images, valid JSON-LD /
  sitemap / robots.
- TODO for Gaffer: designate the release approver and environment gates (who authorizes
  production push, and what evidence — CI run, dry-run output, visual scroll review —
  must be attached).

## Pre-release checklist (from the repo)

From `docs/deployment.md` and `README.md` §17–§19, before every production deployment:

- [ ] `lint` — zero ESLint errors.
- [ ] `build` — zero TypeScript errors, bundle completes.
- [ ] `test` (`node --test app/api/medical-knowledge/route.test.mjs`) and, where
  applicable, `test:e2e` Playwright smoke pass.
- [ ] `deploy:dry-run` passes (`.next/BUILD_ID` present; no server-only names in the
  client bundle).
- [ ] New clinical claims verified by Chief (see authority above).
- [ ] New articles added to `app/insights/data.ts` and `app/sitemap.ts`;
  `public/llms.txt` updated if products/metrics changed; `app/layout.tsx` JSON-LD
  `featureList` updated if capabilities changed.
- [ ] Security headers verified (`curl -I https://sentrahai.com`).
- [ ] Scroll-driven sections visually sanity-checked after layout/animation changes.

## Release record (fill per approved release)

For each release capture: version/commit, scope, changelog entry, verification evidence
(CI run, `deploy:dry-run` output), known risks, approver, target, and rollback /
monitoring outcome. No release-record entries exist in the repo today.

## Rollback (target belum dikonfirmasi / not yet confirmed)

- Per `docs/deployment.md` (Railway): `railway rollback`, or dashboard → Deployments →
  select previous deployment → Redeploy; then re-run the post-deploy `curl` checks.
- Conflicting source: `.agents/HANDOFF.md` (2026-09-26) records re-pointing the Vercel
  project for `sentrahai.com` to the capsule root as the next action. The authoritative
  rollback command depends on the confirmed production target (see "Deployment targets"
  in `docs/OPERATIONS.md`); do not assume either host until the owner confirms.
