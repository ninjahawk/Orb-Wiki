---
title: FAQ
nav_order: 9
---

# FAQ

## Do I need to pay for an AI subscription?
No. Orb works on-device for free, and you can add free API providers and/or run a model on
your own hardware. A paid AI account is one option among several, never a requirement. See
**[Free APIs & Chaining](free-apis.md)**.

## Does it work offline?
Yes — the on-device brain runs with no internet. Some features that need the cloud or your PC
won't be available offline, and Orb will tell you when that's the case rather than failing
silently.

## Will it sound different depending on which model is running?
No. You set Orb's personality once, and it's applied to whatever brain answers. The model is
background infrastructure; the personality is constant. See **[Brains & Models](brains-and-models.md)**.

## Is my data private?
On-device data stays on your device. Connectors only read what you've allowed, only when a
request needs it. If you self-host, the server is *your* machine and you only connect to your
own. Data is shared with a chosen brain only to answer the thing you asked.

## What's the difference between the tiers?
- **On-device:** free, offline, private, always available — lighter capability.
- **Free APIs:** free, more capable, needs a key and a connection.
- **Your own server:** the most powerful — can act on your PC — needs a machine you run it on.

You can use any mix; Orb falls through them automatically.

## Can Orb change things / fix itself?
On a server you host, Orb's backend can do real work on that PC, which makes the whole system
feel self-correcting (fallbacks are automatic, and the backend can adjust itself). The iPhone
app itself never changes its own code — that's both an Apple requirement and by design. The
power lives on your server; the app is the window to it.

## Do I have to set all this up?
No. Install the app and talk to it — that's a complete experience on its own. The APIs,
self-hosting, and local inference are optional upgrades for when you want more power.

## Something's out of date on this wiki.
Free-API limits and provider lists change often. This is a community wiki — please open a PR
to fix it. That's how it stays accurate.

## How do I get help or suggest features?
Open an issue on GitHub. Suggestions for connectors, providers, and workflows are very welcome
— the project gets better with the community.
