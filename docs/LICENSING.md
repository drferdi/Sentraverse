# Licensing and Intellectual Property — Sentraverse

This file summarizes the license posture. The binding text is the existing
[`LICENSE`](../LICENSE) file at the repository root — nothing here grants rights beyond
it.

## Current status (from `LICENSE`)

- Proprietary software license. Copyright `© 2025–2026 Sentra Healthcare Solutions. All
  rights reserved.` Founder & Clinical Steward: Dr. Ferdi Iskandar, S.H., M.Kn., CMDC,
  CLM.
- Unauthorized use strictly prohibited without prior express written permission: no
  copying, reproducing, duplicating, distributing, publishing, transmitting,
  modifying, adapting, translating, reverse-engineering, sublicensing, selling,
  renting, leasing, commercial exploitation, or use to train machine-learning/AI
  systems.
- Permitted use is limited to (a) internal development and review by authorized Sentra
  team members, and (b) security research under a signed responsible-disclosure
  agreement.
- Clinical disclaimer: the software is a clinical decision-support tool, not a certified
  medical device under any regulatory framework (BPOM, Kemenkes, FDA, MDR, or
  equivalent) unless stated in separate regulatory documentation; all clinical outputs
  assist — not replace — licensed healthcare professionals.
- No warranty ("AS IS"); no liability for claims/damages from use or inability to use.
- Contact for commercial licenses or vulnerability reports: email
  `drferdiiskandar@melinda.co.id`, web `https://sentrahai.com`.

## Notes and required confirmations

- `README.md` §25 states `ISC © 2026 Sentra Healthcare Solutions`, and `package.json`
  declares `"license": "ISC"`. These differ from the proprietary `LICENSE` file above,
  which is the binding text in the repo.
- Known mismatch for the owner to fix: `README.md` §25 states `ISC © 2026 Sentra
  Healthcare Solutions` and `package.json` declares `"license": "ISC"`, which
  contradicts the proprietary `LICENSE` file above. The `LICENSE` file is binding;
  the `ISC` references are incorrect and must be corrected by the owner.
- Third-party dependencies are listed in `package.json` (`dependencies` /
  `devDependencies`) with a `pnpm-lock.yaml` and `pnpm-workspace.yaml` overrides; no
  license-attribution inventory exists in the repo.
- Third-party license obligations/attribution, whether any source-available or
  server-side components must remain private, and the authorization required before any
  distribution beyond the permitted uses in `LICENSE`: Belum dikonfirmasi.

A repository being accessible does not make it open-source. Do not describe this
repository as open-source unless the owner replaces `LICENSE` with an approved
open-source text and updates `README.md` and `package.json` to match.
