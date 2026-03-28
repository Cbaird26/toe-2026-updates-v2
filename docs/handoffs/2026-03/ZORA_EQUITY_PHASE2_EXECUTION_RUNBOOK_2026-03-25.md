# Zora Equity Phase 2 Execution Runbook (2026-03-25)

This runbook operationalizes the recommended next step after Phase 1 inventory.

## Decisions locked in this pass

- Canonical integration target: `https://github.com/Cbaird26/zora-equity` (private).
- Source-of-truth strategy: **Option A (Dashboard-first baseline)**.
- Remote safety normalization applied:
  - `zora_trader_minimal` now has:
    - `origin -> https://github.com/Cbaird26/zora-equity.git`
    - `dark-knight -> https://github.com/Cbaird26/Dark-Knight.git`
  - `main` tracks `origin/main`.

## Why Option A

- `zoraasi-dashboard` already hosts the three-layer architecture (Streamlit + FastAPI broker + web shell).
- MQGT-SCF anchor-engine path and tests are already present in that stack.
- `zora_trader_minimal` can be ingested selectively as operator and execution modules rather than replacing the dashboard core.

## Integration boundaries (Phase 2)

### Keep as core in Zora Equity

- dashboard shell and broker APIs from `zoraasi-dashboard`
- Streamlit scanner/research path and MQGT-SCF bridge

### Import selectively from trader fork

- Flask-era operator guardrail semantics
- runtime/session model where still superior
- broker adapter hardening and scripts that still add value

### Defer

- `worldmonitor` integration (reference patterns only for now)
- map-heavy global intelligence surfaces

## Branch and PR sequence (execution recipe)

1. `zoraasi-dashboard` preparation branch
   - branch: `phase2/dashboard-core-import`
   - objective: stage core dashboard tree into `zora-equity` under stable top-level structure.

2. `zora_trader_minimal` extraction branch
   - branch: `phase2/trader-operator-port`
   - objective: port operator/guardrail/runtime elements without replacing dashboard architecture.

3. contract harmonization branch
   - branch: `phase2/env-and-api-contracts`
   - objective: normalize env naming and response contracts (`ZORA_ENABLE_LIVE*`, posture, source health).

4. paper-traceability branch
   - branch: `phase2/paper-traceability`
   - objective: preserve explicit doc links to anchor paper and code module traceability.

5. integration PRs into `zora-equity/main`
   - PR-1: dashboard core import
   - PR-2: trader operator port
   - PR-3: contract harmonization
   - PR-4: traceability/docs hardening

## Safety / publish guardrails

- no secrets from `.env` or local SQLite should ever be committed.
- no force push to `main`.
- preserve `dark-knight` remote as explicit non-origin backup to prevent cross-push confusion.

## Paper anchor reference

- rxiVerse paper (published): [MQGT-SCF as a Minimal Scalar-Singlet EFT](https://rxiverse.org/abs/2603.0088)
