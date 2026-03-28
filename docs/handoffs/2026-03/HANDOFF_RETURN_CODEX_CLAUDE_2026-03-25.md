# Return handoff — Codex + Claude (Zora ecosystem)

Send this file (or the **Ultra-short paste** section at the end) to Codex or Claude when continuing work. It points to deeper docs; it is not a substitute for reading those when changing runtime code.

---

## Authority and safety

- **[SAFETY_CONSTITUTION.md](../../SAFETY_CONSTITUTION.md)** — no `git push`, Zenodo, OSF, or large paid API runs without **explicit human** approval.
- **Repo boundaries are mandatory:** do **not** merge `TradingAgents`, `zora_trader_minimal`, `worldmonitor`, or other products into `zoraasi-dashboard`. Port ideas deliberately; keep separate repos and remotes.
- **Autonomous trading:** paper-first unless there is an explicit live rollout. Local Ollama / veto is **advisory**; it must not invent orders or bypass policy gates.
- **Before any `git remote` change or push:** confirm with the human; verify `git remote -v`.
- **Privacy / vault:** `zoraasi-dashboard` may be **local-only** on a given machine (not a git repo there). These GitHub repos tied to the Finance OS thread are **private**: `Cbaird26/zora-equity`, `Cbaird26/toe-2026-updates`, `Cbaird26/Dark-Knight`, `Cbaird26/TradingAgents`. Treat as vault work; do **not** publish, create remotes, or push without explicit confirmation.

---

## Where to work (local paths)

| Area | Path |
|------|------|
| Zora Finance OS (active shell) | `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard` |
| TradingAgents (sidecar only) | `/Users/christophermichaelbaird/TradingAgents` |
| Flask trader (parallel product) | `/Users/christophermichaelbaird/Projects/zora_trader_minimal` |
| TOE / MQGT handoffs | `/Users/christophermichaelbaird/Downloads/TOE` |

**GitHub:** `Cbaird26/zora-equity` (private coordination), `Cbaird26/toe-2026-updates`, `Cbaird26/Dark-Knight`, and `Cbaird26/TradingAgents` are **private** as of 2026-03-27. Other examples (`worldmonitor`, `zoraasi-suite`, etc.) may remain public or mixed — verify access before assuming. Do not treat any repo as a mandate to collapse codebases.

---

## Canonical deep dives (read before coding)

### Zora Finance OS (dashboard + broker + web)

1. **Full:** `~/Downloads/zoraasi-dashboard/HANDOFF_CURSOR_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`
2. **Short paste:** `~/Downloads/zoraasi-dashboard/HANDOFF_CURSOR_PASTE_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`
3. **Claude prompt blocks:** `~/Downloads/zoraasi-dashboard/HANDOFF_CLAUDE_PROMPT_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md`

Historical (pre–March 27): `HANDOFF_*_2026-03-25_ZORA_FINANCE_OS.md` files in the same directory.

### Repo boundaries + Finance OS links (Codex)

- **Boundaries:** [CODEX_HANDOFF_ZORA_REPO_BOUNDARIES_2026-03-25.md](CODEX_HANDOFF_ZORA_REPO_BOUNDARIES_2026-03-25.md)

### TOE / H1 / MQGT (physics lane — separate from Finance OS)

- **Entry:** [CODEX_HANDOFF.md](../../CODEX_HANDOFF.md)

### Cursor disk / large snapshots

- [CURSOR_IDE_DISK_AND_WORKSPACE.md](CURSOR_IDE_DISK_AND_WORKSPACE.md)

### Developer setup (Finance OS)

- **Start here:** `~/Downloads/zoraasi-dashboard/docs/DEV_START_HERE.md` — Python 3.11, `Makefile` targets (`make broker-install`, `make web-install`, `make broker-test`, etc.).
- **Cursor indexing:** copy `docs/recommended_cursorignore` to `.cursorignore` in each repo root (`zoraasi-dashboard`, `zora_trader_minimal`) if not already present.

### CI (added in recent pass)

- **zoraasi-dashboard:** `.github/workflows/ci.yml` — broker `pytest`, web `npm ci` + `lint` + `build` on `main`/`master`.
- **zora_trader_minimal:** `.github/workflows/ci.yml` + `requirements-ci.txt` + `tests/test_smoke.py` — lightweight `create_app` smoke test (full install remains `requirements.txt`).

### Phase 1 inventory (trading repos — reference only)

- [ZORA_TRADING_PHASE1_INVENTORY_2026-03-25.md](ZORA_TRADING_PHASE1_INVENTORY_2026-03-25.md)

---

## Ultra-short paste (Codex / Claude chat)

```
Zora ecosystem handoff — read TOE docs/handoffs/2026-03/HANDOFF_RETURN_CODEX_CLAUDE_2026-03-25.md for full links.

Finance OS: ~/Downloads/zoraasi-dashboard (may be local-only / not a git repo on this machine). Active stack = FastAPI broker (services/broker) + Vite web (apps/web). Canonical handoffs (2026-03-27 private): HANDOFF_CURSOR_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md, HANDOFF_CURSOR_PASTE_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md, HANDOFF_CLAUDE_PROMPT_2026-03-27_ZORA_FINANCE_OS_PRIVATE.md.

Privacy: Cbaird26/zora-equity, toe-2026-updates, Dark-Knight, TradingAgents are private — no publish/push/remotes without confirmation.

Non-negotiable: do not merge TradingAgents or zora_trader_minimal into the dashboard; paper/demo/shadow automation unless explicit live rollout; Ollama/veto advisory only; 1m lanes do not wait on fresh local inference.

Verified baseline (per March 27 handoff): broker pytest 73 passed; web lint + build passed.

Parallel Flask trader: ~/Projects/zora_trader_minimal. TOE / H1: ~/Downloads/TOE/docs/CODEX_HANDOFF.md. Boundaries: ~/Downloads/TOE/docs/handoffs/2026-03/CODEX_HANDOFF_ZORA_REPO_BOUNDARIES_2026-03-25.md.

Dev quickstart: ~/Downloads/zoraasi-dashboard/docs/DEV_START_HERE.md. Cursor disk: ~/Downloads/TOE/docs/handoffs/2026-03/CURSOR_IDE_DISK_AND_WORKSPACE.md.
```
