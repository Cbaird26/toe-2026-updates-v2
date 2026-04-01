# TradingAgents + Ollama: “does not support tools” vs provider mismatch

If the UI shows **OpenAI** (or another cloud provider) but the run fails with **`gpt-oss:20b-ultra-fast` does not support tools**, the backend actually selected **Ollama** for that model. That model does not expose tool/function calling; the fix is to **use a tool-capable model on the provider you intend** (or disable tools for that run), not to adjust the TOE paper stack.
