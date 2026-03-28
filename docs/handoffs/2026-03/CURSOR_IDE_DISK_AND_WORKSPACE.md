# Cursor IDE disk usage and workspace hygiene

## Symptoms

- macOS reports **Macintosh HD** nearly full.
- Disk utilities show very large **`~/Library/Application Support/Cursor`** usage.
- Typical hot path: `Cursor/snapshots/roots/.../objects/pack` with many multi‑GB `pack-*` files.

## What it is

Cursor stores internal workspace **snapshots** (not your normal Git objects). Large or multi-root workspaces (many `node_modules`, `.venv`, corpora) can inflate this data quickly.

## Safe mitigation (prefer in order)

1. **Quit Cursor** fully (`Cursor` → Quit).
2. **Delete or trim** `~/Library/Application Support/Cursor/snapshots`  
   - Effect: frees the most space; Cursor may re-index workspaces on next open.
3. **Use `.cursorignore`** in each repo root (see `docs/recommended_cursorignore` in `zoraasi-dashboard` and `zora_trader_minimal`: copy to `.cursorignore`).
4. **Shrink workspaces** in Cursor: fewer folders in one multi-root workspace; avoid opening huge trees you do not need indexed.
5. **Other large targets** (unrelated but common): `~/Movies` screen recordings, `~/Downloads`, `~/.ollama` models — review separately.

## What not to do

- Do not delete arbitrary folders under `Application Support/Cursor` while Cursor is running without knowing the impact.
- Do not treat snapshot deletion as a substitute for Git backups; your repos live in normal project paths.

## Related repos

- Zora Finance OS dashboard: `~/Downloads/zoraasi-dashboard/docs/DEV_START_HERE.md`
- Repo boundaries handoff: [CODEX_HANDOFF_ZORA_REPO_BOUNDARIES_2026-03-25.md](CODEX_HANDOFF_ZORA_REPO_BOUNDARIES_2026-03-25.md)
