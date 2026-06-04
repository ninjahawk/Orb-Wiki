---
title: Free APIs & Chaining
nav_order: 4
---

# Free APIs & Chaining

The goal: **effectively unlimited compute, for free.** No single provider gives you
infinite free usage — but if you chain several free providers, Orb falls through to the
next one whenever one runs out. Stack three or four and you rarely hit a wall.

{: .warning }
> Free tiers, rate limits, and model names change *constantly*. Treat every list on this
> page as a starting point and check each provider's own docs for current limits. This is
> a community wiki — if something's out of date, please send a PR.

## How chaining works

Orb tries each brain in order and skips any that are rate-limited or down (for a short
cooldown), then uses the next. The on-device model is always last, so you always get an
answer:

```
free API #1  →  free API #2  →  free API #3  →  on-device floor
```

Order them by what you want first (fastest, or highest-quality) — Orb handles the rest.

## Where you configure it

- **In the app:** Settings → add a provider, paste a key, set the order. Keys are stored
  in your device keychain. (Easiest — start here.)
- **On your own server:** set the `JARVIS_FREE_BACKENDS` environment variable (a JSON
  list). See the format below. (For self-hosters — see **[Self-Hosting](self-hosting.md)**.)

Any provider that speaks the standard **OpenAI Chat Completions** format works — which is
almost all of them.

## Commonly used free / free-tier providers

| Provider | OpenAI-compatible base URL | Notes |
|---|---|---|
| **Groq** | `https://api.groq.com/openai/v1` | Very fast; generous free tier; open models (Llama, etc.) |
| **Google AI Studio (Gemini)** | `https://generativelanguage.googleapis.com/v1beta/openai/` | Large free tier; capable models |
| **Cerebras** | `https://api.cerebras.ai/v1` | Extremely fast; free tier |
| **OpenRouter** | `https://openrouter.ai/api/v1` | Aggregator; many models tagged `:free` |
| **Mistral** | `https://api.mistral.ai/v1` | Free developer tier |
| **GitHub Models** | see GitHub Models docs | Free for developers |
| **Cloudflare Workers AI** | see Cloudflare docs | Free daily allowance |
| **Local (your own hardware)** | `http://<your-pc>:<port>/v1` | Truly free + private — see [Local Inference](local-inference.md) |

Get a key from the provider (usually a free signup), then add it in the app or on your
server.

## Server config format (`JARVIS_FREE_BACKENDS`)

A JSON list, in priority order. Each entry:

```json
[
  {
    "name": "groq",
    "base_url": "https://api.groq.com/openai/v1",
    "model": "llama-3.3-70b-versatile",
    "api_key_env": "GROQ_API_KEY"
  },
  {
    "name": "gemini",
    "base_url": "https://generativelanguage.googleapis.com/v1beta/openai/",
    "model": "gemini-2.0-flash",
    "api_key_env": "GEMINI_API_KEY"
  }
]
```

- `name` — a label for logs.
- `base_url` — the provider's OpenAI-compatible endpoint (no trailing `/chat/completions`;
  Orb appends it).
- `model` — the model id to request.
- `api_key_env` — the **name of an environment variable** that holds the key (so the key
  itself never goes in the config). Set e.g. `GROQ_API_KEY=...` alongside it. Omit this
  field entirely for a keyless local endpoint.

A provider whose key isn't set is automatically skipped — so you can list several and only
fill in the ones you've signed up for.

## Tips for the most free compute

- **Mix fast + capable:** put a fast provider (Groq, Cerebras) first for snappy replies,
  a more capable one next for harder questions.
- **Add a local endpoint last (before on-device):** if you have a PC that can run a model,
  it's free and private — see [Local Inference](local-inference.md).
- **Spread across providers:** several small free tiers chained together outlast any single
  one.
- **Keep keys safe:** never paste a key into a public place. In the app they live in the
  keychain; on a server they live in environment variables, never in the repo.
