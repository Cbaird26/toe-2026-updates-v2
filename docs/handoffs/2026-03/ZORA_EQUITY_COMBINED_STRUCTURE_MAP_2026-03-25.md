# Zora Equity Combined Structure Map (Pre-Move)

This is the pre-migration structure map for combining `zoraasi-dashboard` and selective `zora_trader_minimal` capabilities into `zora-equity`.

## Target Repository Layout

```text
zora-equity/
  README.md
  docs/
    architecture/
      SYSTEM_MAP.md
      SOURCE_BOUNDARIES.md
      ENV_CONTRACT.md
    traceability/
      PAPER_TO_CODE_MAP.md
  apps/
    dashboard-web/                  # from zoraasi-dashboard/apps/web
    scanner-streamlit/              # from zoraasi-dashboard/apps/zora-finance-streamlit
    operator-flask/                 # selective from zora_trader_minimal (deferred import)
  services/
    broker-api/                     # from zoraasi-dashboard/services/broker
    operator-runtime/               # selective shared runtime/session layer
  packages/
    signal-core/                    # classic + mqgt_scf facade/bridge contracts
    risk-guardrails/                # common gating/policy checks
    market-adapters/                # alpaca + optional adapters
    audit-models/                   # shared event/audit schema interfaces
  scripts/
    dev/
    migration/
  tests/
    integration/
```

## Source-to-Target Mapping

### Keep as Core (Dashboard-First)

- `~/Downloads/zoraasi-dashboard/apps/web` -> `apps/dashboard-web`
- `~/Downloads/zoraasi-dashboard/services/broker` -> `services/broker-api`
- `~/Downloads/zoraasi-dashboard/apps/zora-finance-streamlit` -> `apps/scanner-streamlit`

### Import Selectively (Trader Fork)

- `~/Projects/zora_trader_minimal/app.py` and `app/` API posture patterns -> `apps/operator-flask` (or `services/operator-runtime`)
- `~/Projects/zora_trader_minimal` guardrail and session semantics -> `packages/risk-guardrails` + `services/operator-runtime`
- selected CLI checks/scripts -> `scripts/dev` or `scripts/migration`

### Defer for Now

- WorldMonitor code ingestion (architecture-reference only)
- map-heavy intelligence surfaces
- broad geopolitics feed expansion

## Canonical Runtime Surfaces in Combined State

- `apps/dashboard-web`: operator/portfolio UI shell
- `services/broker-api`: trading/account/orders/intraday APIs
- `apps/scanner-streamlit`: research/scanner/backtest surface
- `apps/operator-flask`: optional legacy operator console compatibility layer (only if needed after parity check)

## Contract Alignment Requirements Before Move

1. Env unification (without breaking current behavior):
   - reconcile `ZORA_ENABLE_LIVE_TRADING` and `ZORA_ENABLE_LIVE`
   - preserve broker `LIVE_ARMED` and manual confirmation gates
2. Shared audit vocabulary:
   - align event names for `manual_order`, `strategy_order`, scan/backtest events
3. Signal engine boundary:
   - keep explicit engine mode contract (`classic`, `mqgt_scf`)
4. Operator authorization:
   - preserve localhost + token-gated control semantics from Flask path

## Immediate Move Order (When You Say Go)

1. Import `services/broker-api` and `apps/dashboard-web` into `zora-equity`.
2. Import `apps/scanner-streamlit` and preserve current tests.
3. Port only high-value trader-fork operator/guardrail modules.
4. Add contract docs and integration tests before enabling any shared live path.

## Paper Anchor Traceability Hook

Anchor paper linkage remains pinned to:

- [rxiVerse 2603.0088](https://rxiverse.org/abs/2603.0088)
- scanner engine modules (`mqgt_scf_signal_engine.py`, `engine_bridge.py`)

This structure keeps paper-traceability explicit while preserving advisory/paper-first guardrails.
