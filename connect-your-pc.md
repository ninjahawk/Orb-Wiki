---
title: Connect Your PC
nav_order: 6
---

# Connect Your PC

Once your [Orb server](self-hosting.md) is running, you point the app at it. The app
talks to the server over an encrypted (HTTPS/WSS) connection, so the server needs an
address that supports that — which is exactly what Tailscale gives you for free, in
one command, without opening any ports.

## Pairing the app

In the app: **the menu (☰) → Your PC.** Enter the server's address and its pairing
token, then **Save**. Two rules that prevent nearly every failed pairing:

- **Address = the bare host only** (`yourpc.tail1234.ts.net`) — no `https://`, no
  port, no trailing slash. The app builds the full URLs itself.
- **Paste the token, never retype it.** It's long on purpose; one dropped character
  fails silently. Email or message it to yourself from the PC.

The connection details are stored on your phone and it reconnects on its own from
then on. To switch machines later, just enter a different server. (QR pairing — scan
a code the server displays to fill both fields automatically — is on the way; today
you paste them once.)

## Option A — Private tunnel (recommended)

```powershell
tailscale serve --bg 8340
```

Install [Tailscale](https://tailscale.com) (free) on the PC **and** on your phone,
signed into the same account. Only devices on your private tailnet can reach the
server — nothing is exposed to the internet at all.

- ✅ Reach your Orb from anywhere, on the most private footing available.
- ⚠️ The phone needs the Tailscale app installed and switched on.

## Option B — Public URL

```powershell
tailscale funnel --bg 8340
```

The server gets a public HTTPS URL that works from any network with nothing extra on
the phone. Anyone who somehow learned the URL would still need your token — and you
should make that strict: set `ORB_HTTP_AUTH=1` in the server's `.env` and restart it,
so **every** request requires the token.

- ✅ Works from any network; nothing to install on the phone.
- ⚠️ The URL is publicly reachable — the token (and `ORB_HTTP_AUTH=1`) is the lock.

## What about plain home Wi‑Fi, no Tailscale?

Not today. The app requires an encrypted connection, and a bare local address like
`192.168.x.x` can't provide one — so a direct LAN-only mode isn't currently
supported with the App Store build. Tailscale's private option is the same "only my
devices" result, with encryption handled for you.

## A note on streaming back and forth

The app and your server keep a live two-way connection — your voice and messages go
up, Orb's replies (and visual cards) come back, in real time. Heavier features like
viewing your desktop stream ride the same connection as they roll out.

## Is this allowed on the App Store?

Yes. Connecting an app to a personal server you run is well-established (the same
pattern as SSH clients and self-hosted-app companions). Orb is fully functional on
its own on-device; the server connection is an **optional, clearly-labeled** feature
you configure to your own machine.

## Troubleshooting

- **"Not reachable" right after saving:** it's almost always the address format
  (bare host only) or a mistyped token (paste it). Full checklist:
  [Self-Hosting → If it says "not reachable"](self-hosting.md).
- **Private option not connecting away from home:** the phone's Tailscale app must
  be installed, signed into the same account, and toggled on.
- **Rejected connections:** the server logs every attempt in `backend_err.log`,
  including exactly which check failed — read it before guessing.
