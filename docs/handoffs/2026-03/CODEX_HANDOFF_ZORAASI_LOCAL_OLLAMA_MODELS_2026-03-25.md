# Codex Handoff — Make Zora Finance OS Use Local Ollama Models

Goal: Ensure the **ZoraASI Local Ollama “brain”** is actually working end-to-end inside **Zora Finance OS** (`zoraasi-dashboard`), using the local models we’ve already configured.

Non-negotiable repo rule: do **not** merge/copy code between repos. Fix wiring by configuration + minimal targeted debug only.

---

## 1) Local model names (what we worked on)

From broker settings:

- Ollama base URL: `http://127.0.0.1:11434`
- UI/identity model: `zora-identity` (env: `LOCAL_BRAIN_UI_MODEL`)
- Research/veto model: `gpt-oss:20b-ultra-fast` (env: `LOCAL_BRAIN_RESEARCH_MODEL`)

Code pointers (read these to understand readiness logic and matching):

- Broker config: `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/services/broker/app/config.py`
- Ollama client + readiness logic: `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/services/broker/app/local_brain.py`

---

## 2) Broker endpoints Zora Finance OS uses

The web app’s Terminal workspace calls these endpoints (via `apps/web/src/lib/api.ts` and `TerminalWorkspaceView.tsx`):

- `GET  /api/v1/local-brain/status`
- `GET  /api/v1/local-brain/models`
- `POST /api/v1/local-brain/bench` (role + optional model/prompt)
- `POST /api/v1/local-brain/research` (symbol + timeframe + optional context)

Server routes:

- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/services/broker/app/main.py`

Client wrappers:

- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/apps/web/src/lib/api.ts`
- `/Users/christophermichaelbaird/Downloads/zoraasi-dashboard/apps/web/src/components/TerminalWorkspaceView.tsx`

What “working” means:

- `LocalBrainStatus.reachable = true`
- `LocalBrainStatus.ui_model_available = true`
- `LocalBrainStatus.research_model_available = true`
- `ready_for_ui_chat = true`
- `ready_for_research = true`

---

## 3) Verification checklist (Codex execution recipe)

### A. Confirm Ollama is running + models are loaded

Run:

```bash
ollama list
```

You should see tags that match:

- `zora-identity`
- `gpt-oss:20b-ultra-fast`

If a tag is missing, either:

- pull/create it in Ollama, or
- change `LOCAL_BRAIN_UI_MODEL` / `LOCAL_BRAIN_RESEARCH_MODEL` in your broker `.env` to match the **exact** Ollama tag names.

Reason: the broker checks model availability by matching configured names against `GET /api/tags` from Ollama.

### B. Confirm the broker sees Ollama

With the broker running, call:

```bash
curl http://127.0.0.1:8080/api/v1/local-brain/status
curl http://127.0.0.1:8080/api/v1/local-brain/models
```

Look for:

- `reachable: true`
- `ui_model_available: true`
- `research_model_available: true`
- `ready_for_ui_chat: true`
- `ready_for_research: true`
- if not ready: read `last_error` and `notes`

### C. Confirm the Zora Finance UI can fetch it

1. Start web: `cd apps/web && npm run dev`
2. Open the **Terminal** workspace in the UI.
3. Ensure the “Local brain” section shows status that matches the broker response.

If the broker endpoints work but UI doesn’t update:

- inspect browser network requests to `/api/v1/local-brain/status`
- verify the Vite proxy configuration (web → broker) is correct and broker is reachable from the web runtime.

### D. Bench a local model role (quick smoke)

Run a local benchmark:

```bash
curl -X POST http://127.0.0.1:8080/api/v1/local-brain/bench \
  -H "Content-Type: application/json" \
  -d '{"role":"research","model":"gpt-oss:20b-ultra-fast","prompt":"Say hello and confirm your model role in one short sentence."}'
```

Expected: HTTP 200 with `latency_ms` and `response_preview`.

---

## 4) Minimal code changes (only if config isn’t enough)

Typically you should fix via `.env` / Ollama tags, not code.

If code changes are required, restrict them to:

- surfacing additional info in `LocalBrainStatus` (e.g. show which tags were observed vs configured)
- improving error messages from `LocalBrainManager.get_status()` when `ui_model_available` / `research_model_available` is false

Do not:

- change repo boundaries
- merge any repos
- add secrets to docs

---

## 5) Ultra-short paste for Codex

```
Fix ZoraASI local Ollama usage end-to-end.
Check broker local brain readiness:
  GET /api/v1/local-brain/status and /models must show reachable + ui_model_available + research_model_available.
Configured models are:
  LOCAL_BRAIN_UI_MODEL = zora-identity
  LOCAL_BRAIN_RESEARCH_MODEL = gpt-oss:20b-ultra-fast
If broker shows missing_model, update Ollama tags via `ollama list` (load models) or update .env to match exact tags.
Then confirm the UI Terminal workspace loads Local brain status via apps/web/src/lib/api.ts.
```
