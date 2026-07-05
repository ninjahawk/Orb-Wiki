---
title: Privacy Policy
nav_order: 10
---

# Privacy Policy

**Effective date: July 5, 2026**

Orb is built so that your data stays yours. The app developer runs no server, keeps no
accounts, and collects no personal information. Everything Orb processes happens either on
your own device or on infrastructure you choose and control.

## The short version

- The developer operates **no server** and **collects nothing** about you.
- There is **no analytics, no advertising, and no tracking** of any kind.
- Your voice, your text, and anything Orb reads from your device go only to **your own**
  backend and/or the AI provider **you** configure under your own account — never to the
  developer.

## What Orb processes, and where it goes

**Microphone audio.** Audio is captured only while you are actively using Orb. If you have
connected your own self-hosted Orb backend, that audio is transcribed to text by a speech
model (Whisper) running **on your own machine**. Otherwise, transcription is handled by
Apple's speech recognition (see below). Audio is never sent to, or stored by, the
developer.

**Speech recognition.** Orb uses Apple's **on-device** speech recognition wherever your
device supports it. When on-device recognition is unavailable, Apple may process the audio
on Apple's servers to return the transcript — this is Apple's standard speech service,
governed by Apple's privacy policy, not the developer's.

**Conversation text.** What you say and type is sent to the AI model **you** choose in
Settings: an on-device model, an API provider you configure with your own key/account, or a
model running on your own self-hosted backend. The developer never sees or stores your
conversations. Each provider you enable handles that text under its own privacy policy.

**Calendar, reminders, and contacts (optional).** If you grant access, Orb reads these
**on your device**, and only when a request you make needs them (for example, "what's on my
calendar today"). This information is used to answer you and is never transmitted to the
developer.

**Notifications (optional).** If you enable push notifications, Apple issues a device token
so your own backend can send you alerts through Apple's Push Notification service. The token
and notification content transit Apple's servers, as they do for every iOS app; the
developer runs no push server of their own for the public app.

## What Orb does not do

- **No account, no login.** Orb pairs with your server using a token you generate, not a
  personal profile.
- **No analytics, no crash-tracking, no advertising SDKs, no third-party trackers.**
- **No selling or sharing of your data** — there is no collected data to sell.

## Your control and data deletion

Because nothing is collected centrally, there is no account to close and no developer-held
data to request or delete. To remove everything:

- **Delete the app** to clear all on-device data (settings, pairing token, cached state).
- **Wipe or shut down your own backend** to remove anything stored there — it is your
  machine, entirely under your control.
- **Revoke** microphone, speech, calendar, reminders, or contacts access at any time in
  iOS Settings.

## Third parties

Orb only ever communicates with services **you** choose: the AI provider(s) you configure
and your own backend. Apple provides on-device speech recognition and push delivery as part
of iOS. Each of these operates under its own privacy policy. The developer has no server in
this path and receives none of your data.

## Contact

Questions about privacy? Open an issue on the project's GitHub:
[github.com/ninjahawk/Orb-Wiki/issues](https://github.com/ninjahawk/Orb-Wiki/issues).

## Changes

If this policy changes, the updated version will be posted here with a new effective date.
