> SPS_REVIEW_REQUIRED — this file is an unreviewed scaffold. A repository owner must verify every statement against the sources cited and remove this marker only after review.

# Architecture Decision Records

ADRs record **decisions that were actually made**. Do not fabricate historic decisions
or retroactively claim approvals. New entries follow the repository's established ADR
format.

## Where decisions already live (check these first)

| Location | Content |
| --- | --- |
| `docs/adr-001-nextjs-app-router.md` | Accepted 2026-01-15: Next.js App Router + React 19 (decider: Drferdi, Principal Architect); rationale, consequences, mitigations |
| `.agents/DECISIONS.md` | Append-only capsule log, newest first; e.g. 2026-09-26 migration from `abyss-monorepo` to SAFRS standalone capsule (toolchain pnpm 11.21.0, Node 24) |
| `.agents/HANDOFF.md` | Session handoff (overwritten, not appended); current next action: re-point the Vercel project for `sentrahai.com` to the capsule root (Chief) |
| `ARCHITECTURE.md` + `docs/architecture.md` | Architecture deep-dive + short overview |
| `CHANGELOG.md` | Dated record of notable changes (Keep a Changelog / SemVer), including the 2026-04-18 docs-truth audit |
| `docs/deployment.md` | Deployment decisions as documented (Railway); see `docs/OPERATIONS.md` for the Vercel note in `.agents/HANDOFF.md` |

There is no `docs/adr/` directory in this repo; the only ADR file is
`docs/adr-001-nextjs-app-router.md`. TODO for Gaffer: confirm where future ADRs should
live (same `docs/` level with sequential numbering, or a new `docs/adr/` directory).

## Format for a new ADR (mirrors `docs/adr-001-nextjs-app-router.md`)

- Title, status, date, deciders.
- Context (the problem, with repo evidence).
- Decision (what was chosen).
- Rationale (criterion → reason table).
- Consequences (positive / negative) and mitigations.
- Signature line used by this repo (`_Architected and built by Drferdi …_` is the
  convention in existing docs; `CONTRIBUTING.md` requires `// Architected and built by
  Drferdi.` in new code files).

## Rules

- Durable capsule decisions go to `.agents/DECISIONS.md` (dated heading, decision,
  rationale, evidence); session state goes to `.agents/HANDOFF.md` (overwrite, ~1k
  tokens).
- Clinical-capability claims (e.g. `featureList` in `app/layout.tsx`, demo datasets in
  `SentraSim`/`ClinicalTrajectory`/`ClinicalPrognosis`) require Chief verification
  (`docs/ai-governance.md`, `CONTRIBUTING.md`) — an ADR does not substitute for that
  sign-off.
- TODO for Gaffer: designate the ADR approver and whether ADRs need a second reviewer
  beyond the decider.
