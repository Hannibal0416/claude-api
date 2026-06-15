# claude-api

A small **learning / demo project for the [Anthropic Claude API](https://docs.anthropic.com/) in Python**. It's a starter workspace (managed with [`uv`](https://github.com/astral-sh/uv)) whose real content lives in a Jupyter notebook that walks through the core features of the `anthropic` Python SDK.

This is an educational sandbox — not a deployable application or library.

## Project layout

| File | Purpose |
| --- | --- |
| `claude-api.ipynb` | The heart of the repo — a hands-on notebook demonstrating Claude API usage. |
| `main.py` | A stub entry point that prints `"Hello from claude-api!"`. |
| `pyproject.toml` | Declares the project and its dependencies (`anthropic`, `ipykernel`, `python-dotenv`; Python ≥ 3.13). |
| `uv.lock` | Pinned dependency lockfile for `uv`. |
| `.python-version` | Targets Python 3.13. |
| `.gitignore` | Ignores `.env`, `.venv`, etc. |

## What the notebook teaches

Using `client.messages.create(...)`, the notebook covers:

1. **Basic requests** — load an API key from `.env` via `python-dotenv`, create an `Anthropic()` client, and send a single message.
2. **Multi-turn conversations** — helper functions (`add_user_message`, `add_assistant_message`, `chat`) to build up `messages` history so Claude keeps context across turns.
3. **System prompts** — steering behavior (e.g. a "patient math tutor" persona) via the `system` parameter.
4. **Streaming** — both the raw event stream (`stream=True`) and the higher-level `client.messages.stream(...)` context manager with `stream.text_stream` and `get_final_message()`.
5. **Temperature** — comparing low (`0.0`, predictable) vs. high (`1.0`, creative) sampling.
6. **Stop sequences & response prefilling** — pre-filling the assistant turn (e.g. ` ```json `) and using `stop_sequences=["```"]` to coax Claude into emitting clean, parseable JSON / code blocks.

## Getting started

1. **Install [`uv`](https://github.com/astral-sh/uv)** if you don't have it.

2. **Install dependencies:**

   ```bash
   uv sync
   ```

3. **Add your API key.** Create a `.env` file in the project root:

   ```
   ANTHROPIC_API_KEY=sk-ant-...
   ```

   You can get a key from the [Anthropic Console](https://console.anthropic.com/).

4. **Open the notebook:**

   ```bash
   uv run jupyter lab claude-api.ipynb
   ```

   Or run the stub entry point:

   ```bash
   uv run main.py
   ```

## Note on the model

The notebook currently uses `claude-sonnet-4-0`, which the SDK flags as deprecated (end-of-life June 15, 2026). To keep these examples working, consider migrating to a current model such as `claude-sonnet-4-6` or `claude-opus-4-8`.
