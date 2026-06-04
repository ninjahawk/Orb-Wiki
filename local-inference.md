---
title: Local Inference
nav_order: 7
---

# Local Inference (run a model on your own hardware)

If you have a capable PC — say a gaming machine with a good GPU — you can run an AI model on
it for free and have Orb use it. It's private (nothing leaves your network) and there are no
per-request costs or rate limits.

This works because most local model runners expose the same **OpenAI-compatible** API that
the [free API providers](free-apis.md) do — so to Orb, your gaming PC looks like just another
backend in the chain.

## Pick a runner

Any of these serve an OpenAI-compatible endpoint:

| Runner | Notes |
|---|---|
| **Ollama** | Easiest; one command to pull and serve a model. Endpoint: `http://<pc>:11434/v1` |
| **LM Studio** | Friendly GUI; built-in OpenAI-compatible server. Endpoint: `http://<pc>:1234/v1` |
| **llama.cpp (`llama-server`)** | Lightweight, fast, very configurable |
| **vLLM** | High-throughput; great if you serve multiple requests |

## Connect it to Orb

Add it like any other backend — but with **no API key** (it's your own machine):

- **In the app:** Settings → add a provider → enter the local address, leave the key blank.
- **On your server:** add an entry to `JARVIS_FREE_BACKENDS` with no `api_key_env`:

```json
{
  "name": "gaming-pc",
  "base_url": "http://192.168.1.50:1234/v1",
  "model": "your-local-model-name"
}
```

Replace the address with your PC's local IP and port, and `model` with whatever you loaded.

## Two ways to use it

- **As a backend in the chain:** put your local endpoint near the end of the chain (free and
  private, but slower than the cloud), so it answers when the faster providers are tapped out
  — or first, if you prefer everything stay on your own hardware.
- **Streamed from your PC to your phone:** your PC does the heavy thinking and streams the
  result to your phone over your network (or a [Tailscale tunnel](connect-your-pc.md) from
  anywhere). Your phone stays light; your PC does the work.

## Reaching it from anywhere

On your home Wi‑Fi, the local IP just works. To use your home PC's model while you're out, put
both devices on a [Tailscale](connect-your-pc.md) tunnel and use the tailnet address instead.

## Choosing a model

- Match the model size to your hardware (VRAM). A mid-range GPU runs a solid small/medium model
  smoothly; bigger GPUs run bigger models.
- Prefer recent, instruction-tuned open models for the best assistant feel.
- Remember: Orb keeps *its* personality regardless — the local model is just the engine.
