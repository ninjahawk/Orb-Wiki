---
title: Brains & Models
nav_order: 3
---

# Brains & Models

Orb separates **who it is** (the personality you create) from **what powers it** (the
model). You can swap the model freely; the personality is constant. This is why Orb
feels like one assistant no matter what's running underneath.

## The tiers

### On-device (always available)
A compact model runs directly on your phone. No internet, no account, no key. It's the
floor that's *always there* — fast for everyday things, and the reason Orb works on a
plane or with no signal. It's deliberately honest about what it can and can't do
locally, and will offer to hand bigger jobs to a stronger brain when one is connected.

### Free APIs (chained)
Add one or more free cloud providers and Orb rotates through them automatically: when
one hits its limit, it falls through to the next. Stack a few and you have a lot of
free capability. Setup: **[Free APIs & Chaining](free-apis.md)**.

### Your own server
Run the Orb server on a PC for the most capable tier — including doing real things on
that computer. Setup: **[Self-Hosting](self-hosting.md)**.

## How Orb stays consistent

Whichever tier answers, Orb is fed the **same personality** you set up. The model is
background infrastructure. So:

- Switching brains doesn't change *who* Orb is — only how much it can do.
- A weaker brain doesn't get a different attitude; it just has fewer abilities, and
  says so.
- You can let Orb pick the best available brain automatically, or pin one in Settings.

## Falling through, gracefully

The chain is ordered by capability and availability. A turn flows down the chain until
something answers:

```
your own server  →  free API #1  →  free API #2  →  … →  on-device floor
```

If a server or API is unreachable or rate-limited, Orb skips it for a short cooldown and
uses the next one — you just get an answer. The on-device floor never gets skipped, so a
request never dead-ends.

> **The point:** you set this up once and then forget it exists. Orb just works, and it
> appears to fix itself because the fallbacks are automatic.
