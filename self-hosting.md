---
title: Self-Hosting
nav_order: 5
---

# Self-Hosting Your Own Orb Server

The Orb server is the most powerful brain tier. It runs on a PC you own and can do real
things on that machine — and you reach it from your phone, at home or anywhere.

{: .important }
> **You only ever connect to your own server.** A running Orb server acts *as you* on that
> computer — it can use the apps, files, and accounts that machine is logged into. So treat
> a server URL like a key to that computer: only connect the app to a machine you control.

## What the server adds

- Real desktop actions on *your* PC (open things, media, and more as features land).
- The most capable brains, including connecting your own AI accounts and local models.
- A persistent presence that's always reachable from your phone.

## Requirements

- A PC (Windows today; more platforms over time).
- A few minutes to run the setup script.
- Optional: a free [Tailscale](https://tailscale.com) account if you want to reach your
  server from outside your home network (see **[Connect Your PC](connect-your-pc.md)**).

## Install (overview)

1. Get the Orb server: clone **[github.com/getorb/Orb-Backend](https://github.com/getorb/Orb-Backend)**,
   then follow its `README` — the guided **`SETUP.md`** (Claude Code walks you through it) or
   the fully manual **`SELF_HOSTING.md`**.
2. Run the one-time setup (installs dependencies).
3. Start the server. On first run it generates a **unique pairing token** for your install.
4. Pair your phone: scan the QR code the server shows (or enter the URL + token by hand).
   See **[Connect Your PC](connect-your-pc.md)**.

That's it — your phone now talks to your server.

## Choosing the server's brain

Your server can use, in order of your choosing:

- **Your own AI account** (if you have one logged in on that PC), and/or
- **Free APIs** you've configured via `JARVIS_FREE_BACKENDS` — see
  **[Free APIs & Chaining](free-apis.md)**, and/or
- **A local model** running on that PC or another machine on your network — see
  **[Local Inference](local-inference.md)**, and/or
- The on-device floor on the phone, always, as the final fallback.

You don't need an AI subscription to self-host — a server running purely on free APIs and/or
a local model works fine.

## Security basics

- **Per-install token.** Each server generates its own token; pairing carries it to your
  phone. Don't share it.
- **No secrets in the open.** Your keys live in environment variables / your device keychain,
  never in shared files.
- **Stay on your own network or a private tunnel.** Use your home Wi‑Fi (LAN) or a private
  tunnel like Tailscale rather than exposing the server to the open internet. Details:
  **[Connect Your PC](connect-your-pc.md)**.
- **It's your machine.** The server can act on the computer it runs on — which is exactly the
  power you want, and exactly why you only connect to your own.
