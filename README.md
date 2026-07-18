# LLM — Private, On-Device AI Chat

**A complete AI chat that runs entirely on your Android phone. No account, no cloud, no data ever leaves your device.** You bring the model file; the app does the rest — offline, private, and yours.

> Everything happens locally. Your conversations, characters and files stay on your phone. There is no sign-up, no server, no tracking, and nothing to lose access to.

> 💸 It runs offline so nobody can bill you — which is exactly why nobody bills me. Tip if it earned it:
>
> **PayPal** — paypal.me/FAMarco
>
> **Bitcoin** — `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

## What is it?

LLM is a self-contained AI chat app for Android. Point it at a model file you already have and start talking — the whole assistant lives on your device. It is built for people who want the power of a modern chat assistant without handing their words to someone else's computer.

No internet connection is required to use it. Airplane mode works perfectly.

## Why you can trust it

- **Fully offline.** The app works with no network at all. Your messages are generated on your own hardware.
- **Nothing leaves your phone.** Chats, characters, imported files and settings are stored only in local app storage.
- **No account, ever.** There is nothing to register, nothing to log in to, and no profile to build.
- **No lock-in.** Your data is yours. Export it whenever you want and take it with you.

## Get it

1. Download the latest release from the [Releases](../../releases) page — see the [changelog](CHANGELOG.md) for what changed.
2. Allow installation from your browser or file manager if Android asks.
3. Open the app, add a model file, and start chatting.

> **Updating:** if you already have v0.14.2 or newer, this installs straight on top and keeps your chats. Coming from anything older than v0.14.2, uninstall once first — the signing key changed in that release.

## Verify what you downloaded

Every release lists the exact fingerprint of its installer so you can confirm the file is genuine and untampered before installing.

```
SHA-256:  d04976df6e95fac7986310a1001c9a2023aa7e2278dbbfc4f713a96dcee03fbe
```

On Windows PowerShell:

```powershell
Get-FileHash .\LLM-v0.14.4-arm64.apk -Algorithm SHA256
```

The value you get must match the one in the release notes exactly. If it does not, do not install the file.

## Features

### Private conversations
Natural, flowing chat with your own model, with saved history that stays on your device. Pick up any conversation where you left off.

### Characters and roleplay
Six characters are built in and ready the moment you open the app — an engineer, an analyst, a teacher, a writer, a philosopher and one deeply sarcastic machine. Tap any of them to start a chat where they greet you and stay in role. Import your own character cards alongside them, kept in their own section so they never get lost among the built-ins. A set of ready-made behaviour presets lets you shape the assistant from strictly safe to completely unrestricted, and you can write your own.

### Long answers, uninterrupted
When a reply is long, the app keeps it going on its own instead of stopping halfway — you get the whole answer without prompting for more.

### Fast on modern phones
On newer devices the app uses on-device acceleration to answer faster, and picks the right setting for each model automatically — no tuning required.

### Made to read comfortably
A clean, modern interface with light and dark modes, adjustable text and spacing, high-contrast and reduced-motion options, and a range of accent colours to make it yours. Answers render properly — including tables — and a built-in Help section explains the options in plain language.

### Your own local API
Turn your phone into a private AI endpoint on your home network, so your other apps and devices can use your on-device assistant — still without touching the cloud.

### Safe by default
Optional app lock with PIN or fingerprint, encrypted backups, and a private-screen mode keep your conversations for your eyes only.

## System requirements

- A modern Android phone with enough memory and storage for the model file you intend to run.
- A compatible model file (which you provide).
- No internet connection required.

## License

Proprietary. All rights reserved. This repository contains the app's public documentation and releases only; the source code is not open.

© eVersor-HN
