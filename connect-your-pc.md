---
title: Connect Your PC
nav_order: 6
---

# Connect Your PC

Once your [Orb server](self-hosting.md) is running, you point the app at it. There are two
ways to reach it, depending on whether you want it only at home or from anywhere.

## Pairing the app

In the app: **Settings → Your Server → Connect.** Then either:

- **Scan the QR code** the server displays — this fills in the address and pairing token
  automatically (the easy way), or
- **Enter the address by hand** — the server URL plus the pairing token.

Your phone stores the connection securely (in the keychain) and reconnects on its own from
then on. To switch machines later, just connect to a different server.

## Option A — Home network (LAN), zero setup

If your phone and PC are on the **same Wi‑Fi**, the app can talk to the server directly over
your local network using the PC's local address (something like `192.168.x.x`). Nothing to
install — it just works at home.

- ✅ Simplest possible setup.
- ⚠️ Only works while you're on the same network as the PC.

## Option B — Anywhere, via a private tunnel (Tailscale)

To reach your server when you're *away* from home, use a private tunnel. We recommend
[**Tailscale**](https://tailscale.com) — it's free for personal use and creates a secure
private network between your devices without opening any ports to the public internet.

1. Install Tailscale on the PC and on your phone, sign in to both with the same account.
2. The PC gets a stable private address on your "tailnet."
3. Point the app at that address (or scan the QR — the server can show its tailnet address).

- ✅ Reach your Orb from anywhere, securely.
- ✅ No ports exposed to the open internet; only your own devices can connect.
- ⚠️ One-time install of Tailscale on both devices.

## A note on streaming back and forth

The app and your server keep a live two-way connection — your voice and messages go up, Orb's
replies (and visual cards) come back, in real time. Heavier features like viewing your desktop
stream ride the same connection as they roll out.

## Is this allowed on the App Store?

Yes. Connecting an app to a personal server you run is well-established (the same pattern as
SSH clients and self-hosted-app companions). Orb is fully functional on its own on-device; the
server connection is an **optional, clearly-labeled** advanced feature you configure to your own
machine. Nothing about your server's capabilities is hidden or misrepresented in the app.

## Troubleshooting

- **Can't connect on LAN:** make sure both devices are on the same Wi‑Fi and the server is
  running. Some routers isolate devices ("AP isolation") — turn that off, or use Tailscale.
- **Can't connect away from home:** you need a tunnel (Option B). A bare home IP won't be
  reachable from outside without one.
- **"Unauthorized":** the pairing token is wrong or stale — re-scan the QR / re-pair.
