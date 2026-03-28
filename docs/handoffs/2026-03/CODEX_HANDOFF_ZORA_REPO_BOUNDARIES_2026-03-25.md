# Codex Handoff - Zora Repo Boundaries (2026-03-25)

**Unified return handoff (Codex + Claude):** [HANDOFF_RETURN_CODEX_CLAUDE_2026-03-25.md](HANDOFF_RETURN_CODEX_CLAUDE_2026-03-25.md)

## Privacy / March 27 (2026)

As of 2026-03-27, these GitHub repositories tied to the Zora Finance OS / trading thread are **private**:

- `Cbaird26/zora-equity`
- `Cbaird26/toe-2026-updates`
- `Cbaird26/Dark-Knight`
- `Cbaird26/TradingAgents`

`zoraasi-dashboard` at `~/Downloads/zoraasi-dashboard` may be **local-only** on a machine (not initialized as git there). Treat the stack as vault work: no publish, new remotes, or push without explicit human confirmation.

**Canonical Finance OS handoffs (private state, current runtime):**

- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/HANDOFF_CURSOR_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`
- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/HANDOFF_CURSOR_PASTE_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`
- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/HANDOFF_CLAUDE_PROMPT_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`

## Current Intent (Authoritative)

The user wants to keep all repos separate. Do **not** collapse repos into one another.

Keep these as distinct products/workstreams:

- `zoraasi-dashboard`
- `zora_trader_minimal`
- `worldmonitor`
- `Dark-Knight`
- `zora-equity` (coordination/meta layer, not a forced monorepo merge target)

## What Happened In This Session

1. Phase 1 inventory/reporting was completed.
2. A private GitHub repo was created:
   - `https://github.com/Cbaird26/zora-equity`
3. `zora_trader_minimal` git remotes were changed for safety:
   - `origin -> https://github.com/Cbaird26/zora-equity.git`
   - `dark-knight -> https://github.com/Cbaird26/Dark-Knight.git`
4. Integration/mapping docs were drafted, but user clarified they do **not** want repo collapse.

## Critical Correction To Honor Going Forward

Treat prior "merge/integration into one repo" artifacts as exploratory only.

Do not execute any workflow that:

- imports one repo's full codebase into another by default
- replaces per-repo ownership with a single trunk
- pushes code across repos without explicit per-repo approval

## Immediate Safe Next Step

Before any new code migration:

1. Ask user what `origin` should be for each repo (especially `zora_trader_minimal`).
2. Keep `zora-equity` as optional coordination repo:
   - architecture docs
   - cross-repo contracts
   - roadmap/checklists
3. Use per-repo PRs, one repo at a time.

## Files Created In This Session (Context)

- `docs/handoffs/2026-03/ZORA_TRADING_PHASE1_INVENTORY_2026-03-25.md`
- `docs/handoffs/2026-03/ZORA_EQUITY_PHASE2_EXECUTION_RUNBOOK_2026-03-25.md`
- `docs/handoffs/2026-03/ZORA_EQUITY_COMBINED_STRUCTURE_MAP_2026-03-25.md`
- `docs/handoffs/2026-03/CODEX_HANDOFF_ZORA_REPO_BOUNDARIES_2026-03-25.md` (this file)

## Operational Rules For Next Codex Agent

- Preserve repo boundaries first.
- Prefer documentation and contract alignment over code migration.
- If asked to connect repos, do it with references/interfaces, not code collapse.
- Confirm before any remote change, branch push, or cross-repo copy.

## Zora Finance OS (zoraasi-dashboard)

Canonical Cursor/Claude handoffs for the **active** Finance OS runtime (FastAPI broker + Vite web, agent runtime, TradingAgents sidecar, local Ollama brain, venue attachments) — **2026-03-27 private** (see **Privacy / March 27** above):

- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/HANDOFF_CURSOR_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`
- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/HANDOFF_CURSOR_PASTE_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`
- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/HANDOFF_CLAUDE_PROMPT_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`

Historical: `HANDOFF_*_2026-03-25_ZORA_FINANCE_OS.md` in the same directory.

Do **not** collapse other repos into `zoraasi-dashboard`. Keep autonomous trading **paper-only** unless there is explicit live rollout approval; local brain / veto remains advisory and must not invent orders.

**Cursor disk / snapshots:** [CURSOR_IDE_DISK_AND_WORKSPACE.md](CURSOR_IDE_DISK_AND_WORKSPACE.md)
