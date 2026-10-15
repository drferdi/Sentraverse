> SPS_REVIEW_REQUIRED — this file is an unreviewed scaffold. A repository owner must verify every statement against the sources cited and remove this marker only after review.

# Repository Ownership and Governance — Sentraverse

## Authority (facts in the repo)

- **Human owner:** Chief (dr. Ferdi Iskandar) — `AGENTS.md` ("Objective and ownership"),
  `project.contract.json` (`owner`), `.agents/CONTEXT.md`.
- **Default risk:** `R1`. Breaking public routes or the `/dashboard` and `/asisten-medis`
  rewrites needs review (`AGENTS.md`).
- **Clinical content authority:** all clinical claims (statistics, accuracy metrics, demo
  dataset values in `SentraSim`, `ClinicalTrajectory`, `ClinicalPrognosis`, copy in
  `app/insights/data.ts`, `components/Services.tsx`, `components/Hero.tsx`) must be
  verified by Chief (Dr. Ferdi Iskandar) before merge/publication (`CONTRIBUTING.md`
  "Clinical Content Policy", `docs/ai-governance.md`, `.github/PULL_REQUEST_TEMPLATE.md`
  content checklist).
- **Protected areas:** security headers and rewrites in `next.config.mjs`;
  `/api/medical-knowledge` (`.agents/CONTEXT.md`). The PR template additionally requires
  review for changes to `headers()` security configuration and `remotePatterns`
  (`next.config.mjs`).
- **Security reports:** privately to `drferdiiskandar@melinda.co.id` with subject
  `[SECURITY] sentra-main — <brief description>`; no public GitHub issue; 48-hour
  acknowledgement, 90-day remediation window requested (`SECURITY.md`).
- **License contact:** `LICENSE` names Sentra Healthcare Solutions, founder & clinical
  steward Dr. Ferdi Iskandar, contact `drferdiiskandar@melinda.co.id` /
  `https://sentrahai.com` (see `docs/LICENSING.md`).

## Module and path stewardship (from repo structure)

- Public routes and composition: `app/` (landing `app/page.tsx`, `story`, `insights`,
  `sentrapedia`, `ekosistem`, `sentrawiki`, `privacy`, `terms`, `api/`).
- Section and showcase components: `components/` (including `blueprint-story/`,
  `sentrasim/`, `sentrapedia/`, `sentrawiki/`, `ekosistem/`, `ui/`).
- Governance primitives: `lib/design-governance.ts`, `lib/site-links.ts` (internal link
  single source of truth), `lib/use-smooth-scroll.ts`, `lib/utils.ts`.
- Docs: root `README.md`, `ARCHITECTURE.md`, `CHANGELOG.md`, `CONTRIBUTING.md`,
  `SECURITY.md`, `ROADMAP.md`, plus `docs/` index (`docs/README.md`). Durable capsule
  decisions: `.agents/DECISIONS.md`.

TODO for Gaffer: confirm per-module maintainers (if any beyond the owner above), the
security contact for non-vulnerability governance questions, and the escalation channel.

## Collaboration rules

- This capsule owns its runtime (own pnpm workspace, lockfile, scripts, build config)
  and never depends on another capsule; do not modify other capsules or shared packages
  without recording scope expansion (`AGENTS.md`).
- `CONTRIBUTING.md` workflow: branch from `main`, `lint` with zero errors, `build`
  without TypeScript errors, open a PR against `main` with the template completed;
  commit format `type(scope): description` (`feat`, `fix`, `content`, `style`,
  `refactor`, `docs`, `chore`, `perf`).
- CI (`.github/workflows/ci.yml`): on push to `main`/`master`/`claude/**`/`feature/**`
  and on PRs to `main`/`master`, `lint` must pass before `build` runs
  (pnpm `11.21.0`, Node `24`, `pnpm install --frozen-lockfile`).
- Documentation improvements do not grant permission to modify software, CI, secrets, or
  deployment configuration.

TODO for Gaffer: confirm branch/merge rules (required reviewers, protected paths beyond
`next.config.mjs` and `/api/medical-knowledge`, merge vs. squash policy) — the repo
states the PR template and CI gates but no explicit branch-protection settings.
