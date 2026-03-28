# Zora Trading Ecosystem - Phase 1 Inventory (2026-03-25)

This is an inventory-only mapping pass across the requested repos and paper linkage, with no merges, no file moves, and no pushes.

## 1) Canonical Repo Map (Local + GitHub)

| Target | Local path / state | GitHub state | Notes |
|---|---|---|---|
| `zoraasi-dashboard` | `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard` exists; **not a git repo** (`.git/config` missing) | `Cbaird26/zoraasi-dashboard` not found | Active local product tree (Streamlit + broker + web), local-first posture. |
| `zora_trader_minimal` (trading fork) | `/Users/christophermichaelbaird/Projects/zora_trader_minimal` exists; branch `main`; very dirty working tree | No `Cbaird26/zora_trader_minimal` found | **Remote mismatch risk:** local `origin` points to `https://github.com/Cbaird26/Dark-Knight.git`. |
| `Dark-Knight` | No confirmed local clone found in checked paths | `Cbaird26/Dark-Knight` public, default `main`, updated `2026-03-25` | Project description: "Project: Dark Knight". |
| `WorldMonitor` | No confirmed local clone found in checked paths | `Cbaird26/worldmonitor` public, default `main`, updated `2026-03-24` | Public repo exists and is active; issues are disabled. |
| legacy `zora-asi` | No local `zora-asi` path confirmed from scanned candidates | No exact `zora-asi` repo found under account | Closest lineage candidates on GitHub: `zoraasi-suite`, `local-asi` (private). |
| `Zora Equity` | No local path confirmed (`zora-equity` / `ZoraEquity` not found) | No `Cbaird26/zora-equity` found | Integration target likely conceptual/new repo not yet created under this exact name. |

## 2) Public GitHub Snapshot (Requested Domain)

Confirmed public repos relevant to this phase:

- `Cbaird26/Dark-Knight`
  - visibility: public
  - default branch: `main`
  - open PRs: `0`
  - open issues: `0`
- `Cbaird26/worldmonitor`
  - visibility: public
  - default branch: `main`
  - open PRs: `0`
  - issues: disabled
- `Cbaird26/zoraasi-suite`
  - visibility: public
  - default branch: `main`
  - open PRs: `4` (all from `Cbaird26`, mostly "Zora agentic control")
  - open issues: `0`

Lineage/duplicate observations:

- The requested names (`zoraasi-dashboard`, `zora_trader_minimal`, `zora-equity`) are **not present** as exact GitHub repos under `Cbaird26`.
- The likely "legacy zora-asi family" appears split across:
  - `zoraasi-suite` (public)
  - `local-asi` (private)
  - plus active local-only trees.

## 3) Architecture and Overlap Matrix

| Surface | Primary role | Runtime | Persistence | Trading posture |
|---|---|---|---|---|
| `zoraasi-dashboard` | Multi-surface platform: Streamlit scanner + FastAPI broker + Vite app | Streamlit `:8501`, broker `:8080`, web `:5173` | SQLite audit DB + local data | Advisory-first, paper-first, explicit live gates |
| `zora_trader_minimal` | Flask operator console | Flask `:5010` | SQLite runtime store | Paper-first with env/token gates |
| `worldmonitor` | Real-time global intelligence dashboard | (repo-defined, not locally validated in this pass) | (repo-defined) | Not primary trading engine |
| `Dark-Knight` | Public project shell currently wired as `origin` for local trader repo | (not locally validated in this pass) | (not locally validated in this pass) | Unknown from this pass |

Overlap likely to reconcile in future integration:

- UI/control surfaces: Flask operator console vs React/Streamlit operator + scanner workflows.
- Execution adapter boundaries: both trading surfaces include paper/live gating semantics and operator controls.
- Env schema divergence: `ZORA_ENABLE_LIVE_TRADING` (Flask) vs `ZORA_ENABLE_LIVE`/broker flags (dashboard stack).
- Data store split: separate SQLite stores and audit/event models.

## 4) Risk Zones (Prioritized)

1. **Critical lineage risk - wrong remote on active local trader repo**
   - `/Users/christophermichaelbaird/Projects/zora_trader_minimal/.git/config` points `origin` to `Cbaird26/Dark-Knight`.
   - Any push from `zora_trader_minimal` can land in the wrong public repo unless remotes are corrected.

2. **Name-to-repo ambiguity**
   - Desired integration target (`Zora Equity`) and intended source repos are partly conceptual vs concrete GitHub names.
   - Raises branch/PR targeting risk for Phase 2.

3. **Divergent runtime contracts**
   - Parallel stacks are intentional, but merge without contract mapping risks breaking auth, env gating, and operator workflows.

4. **Paper mapping ambiguity**
   - Anchor engine is present and tested in dashboard stack, but production-path vs optional-path boundaries must stay explicit during integration.

## 5) Paper-to-Repo Traceability

Confirmed anchors in active local code:

- `apps/zora-finance-streamlit/mqgt_scf_signal_engine.py`
  - Explicitly maps anchor equations (`Phi_c`, `E`, Born tilt, GKSL decay) to advisory signal generation.
  - Includes safety invariants and paper references in module docs.
- `apps/zora-finance-streamlit/tests/test_mqgt_scf_signal_engine.py`
  - Smoke tests covering bounded field outputs and signal generation contract.
- `HANDOFF_CURSOR_CLAUDE.md`
  - Documents dual-engine approach (`classic` + `mqgt_scf`) and bridge pattern.

Classification of appearances:

- **Production-optional path:** `mqgt_scf_signal_engine.py` via engine toggle/bridge.
- **Test path:** `tests/test_mqgt_scf_signal_engine.py`.
- **Documentation path:** handoff + ecosystem docs describing parallel stacks and safety posture.

## 6) Ready / Not-Ready for Zora Equity Integration

Ready now:

- Canonical understanding that `zoraasi-dashboard` and `zora_trader_minimal` are parallel, not merged.
- Confirmed public repos for `Dark-Knight`, `worldmonitor`, and `zoraasi-suite`.
- Identified key contract/risk boundaries.

Not ready yet:

- No confirmed concrete `Zora Equity` repo (local or GitHub exact-name match).
- `zora_trader_minimal` remote must be normalized before any integration/publish workflow.
- Local presence of `WorldMonitor` and legacy `zora-asi` trees not fully enumerated in this pass due path discovery limits in the current session.

## 7) Phase 2 Option Set (No Execution Yet)

- **Option A - Dashboard-first integration baseline**
  - Treat `zoraasi-dashboard` as source-of-truth product core.
  - Import only selected trader operator capabilities from Flask stack.

- **Option B - Trader-first baseline**
  - Treat `zora_trader_minimal` as execution spine.
  - Add scanner/world context as sidecars.

- **Option C - Clean-room Zora Equity shell**
  - Stand up new `zora-equity` repo with explicit submodule/subtree or package boundaries.
  - Migrate features intentionally behind stable contracts.

Recommended next step before Phase 2 implementation:

1) confirm/create canonical `Zora Equity` repo name and visibility;  
2) correct remotes for `zora_trader_minimal`;  
3) choose Option A/B/C as the integration boundary strategy.
