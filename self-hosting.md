---
title: Self-Hosting
nav_order: 5
---

# Run Your Own Orb Server

One page, zero to paired. About 15 minutes on a Windows PC. Every command below is
copy-pasteable and this exact sequence is tested end-to-end.

The server is the open-source half of Orb:
**[github.com/getorb/Orb-Backend](https://github.com/getorb/Orb-Backend)** (MIT).
The [app](https://apps.apple.com/us/app/orb-ai/id6776376035) works on its own —
the server is what gives it hands, memory, and a machine that works for you while
your phone is in your pocket.

{: .important }
> **You only ever connect to your own server.** A running Orb server acts *as you* on
> that computer. Treat its address + token like a key to that machine: never share them,
> never connect the app to a server you don't control.

## What you need

- A **Windows PC** that stays on (macOS backend is planned, not here yet).
- **[Python 3.11+](https://www.python.org/downloads/)** and
  **[Git](https://git-scm.com/download/win)** — both free. When installing Python,
  tick *"Add python.exe to PATH."*
- **A brain.** Pick at least one:
  - **[Claude Code](https://docs.anthropic.com/en/docs/claude-code)** installed and
    logged in on the PC (recommended — the server talks to Claude through your own
    login; no API key). Uses your existing Claude subscription.
  - Any OpenAI-compatible **free API** — see [Free APIs & Chaining](free-apis.md).
  - A **local model** via Ollama — see [Local Inference](local-inference.md).
- **[Tailscale](https://tailscale.com)** (free) — to reach the server from your phone.

## Step 1 — Get the server onto the PC

Open PowerShell and run:

```powershell
git clone https://github.com/getorb/Orb-Backend
cd Orb-Backend
python -m venv venv
venv\Scripts\pip install -r requirements.txt
```

## Step 2 — Run the setup wizard

```powershell
venv\Scripts\python scripts\setup.py
```

It asks your name, your city (for weather), whether to set up push (say `n` — it's
optional and needs a paid Apple developer account), and offers a boot check. It writes
a `.env` file containing your unique pairing token (`ORB_TOKEN`).

**Send that token to your phone now** — email or message it to yourself. It's long;
you'll want to paste it in Step 5, not type it.

## Step 3 — Start the server

```powershell
venv\Scripts\python supervisor.py
```

Open <http://localhost:8340/api/health> in a browser on the PC — you should see
`"status": "online"`. Leave the server running (the supervisor restarts it if it
ever crashes).

## Step 4 — Give it an address your phone can reach

Install Tailscale on the PC and sign in, then pick one:

**Private (recommended)** — only your own devices can reach it:

```powershell
tailscale serve --bg 8340
```

Also install the Tailscale app on your iPhone and sign in with the **same account**.

**Public URL** — reachable from any network, no Tailscale app needed on the phone:

```powershell
tailscale funnel --bg 8340
```

If you choose public, also open `.env`, set `ORB_HTTP_AUTH=1`, and restart the
server — that makes the token required on every request, not just voice.

Either way Tailscale prints your address, something like
`https://yourpc.tail1234.ts.net`. The part you need is just the host:
`yourpc.tail1234.ts.net`.

## Step 5 — Pair the app

In the Orb app: **menu (☰) → Your PC.**

1. **Server address:** the bare host only — `yourpc.tail1234.ts.net`.
   **No `https://`, no port, no trailing slash.** The app adds those itself;
   including them is the #1 cause of "not reachable."
2. **Token:** paste the `ORB_TOKEN` value from Step 2 exactly. **Paste, don't
   retype** — a single dropped character fails silently.
3. Tap **Save**. (Tip: if you *just* launched the app, give it a few seconds on the
   home screen first, then save.)

The status turns connected, and that's it — talk to it. Your phone reconnects on its
own from now on, from anywhere your chosen option covers.

## If it says "not reachable"

Work down this list — it is almost always #1 or #2:

1. **Address format.** Bare host only. Delete any `https://`, `:8340`, or `/`.
2. **Token.** Paste it fresh from `.env` (in the folder you cloned). Compare the
   last four characters.
3. **Private mode?** The phone must have the Tailscale app installed, signed into
   the same account, and toggled on.
4. **Server up?** `http://localhost:8340/api/health` on the PC must answer.
5. **See what the server saw.** Every connection attempt is logged in
   `backend_err.log` in the server folder — a rejected attempt shows exactly which
   check failed (`token_match=False` means the token the phone sent didn't match).

## Prefer to not do any of this by hand?

If you installed Claude Code for the brain, it can also do the setup: run `claude`
inside the `Orb-Backend` folder and say **"Set up the Orb backend for me, then help
me connect my phone."** The repository teaches it the entire flow, this page
included. Any capable AI agent on your PC can follow this page the same way.

## Going deeper

- **[SELF_HOSTING.md](https://github.com/getorb/Orb-Backend/blob/main/SELF_HOSTING.md)**
  — every setting, push notifications, Gmail, watchers, all of it.
- **[API.md](https://github.com/getorb/Orb-Backend/blob/main/API.md)** — the
  WebSocket + HTTP surface, if you want to build your own client.
- [Connect Your PC](connect-your-pc.md) — more on reachability choices.
- [Free APIs & Chaining](free-apis.md) · [Local Inference](local-inference.md) —
  running with no paid AI account at all.
