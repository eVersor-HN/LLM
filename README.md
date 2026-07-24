# LLM — Private, On-Device AI Chat

**A complete AI chat that runs entirely on your Android phone. No account, no cloud, no telemetry.** You bring the model file; the app does the rest — offline, private, and yours.

> Everything happens locally. Your conversations, characters and files stay on your phone. There is no sign-up, no tracking, and nothing to lose access to. The app makes no network connection at all unless you switch on one of the optional online features — see [What talks to the internet](#what-talks-to-the-internet) below. Both are off by default.

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

- **Offline by default.** Out of the box the app makes no network connection at all. Your messages are generated on your own hardware.
- **Your data stays local.** Chats, characters, imported files and settings are stored only in local app storage, encrypted at rest.
- **No account, ever.** There is nothing to register, nothing to log in to, and no profile to build.
- **No telemetry.** No analytics, no crash reporting, no phone-home — not even an optional one.
- **No lock-in.** Your data is yours. Export it whenever you want and take it with you.

## What talks to the internet

Two features can send data off the device. **Both are disabled by default and each takes several deliberate steps to switch on.** Everything else — the model, your chats, your characters — never touches a network.

- **Web search, open webpage, crawl.** If you enable them in Settings → Tools and model actions, the model can ask to run a search. Your **query text** is then sent to the search provider you configured: either your own [SearXNG](https://searx.space) instance, or the Brave Search API. Opening a webpage fetches that page directly. Your chat history and system prompt are never sent — only the query or the URL. Every request is shown to you for approval before it runs.
- **Local API server.** An optional OpenAI-compatible server for other apps on your own network (Settings → Local API server). It binds to loopback by default; LAN mode requires a generated bearer token. Traffic on your LAN is plain HTTP, so treat it as you would any local development server.

If you never enable either, the app never opens a socket.

## Get it

1. Download the latest release from the [Releases](../../releases) page — see the [changelog](CHANGELOG.md) for what changed.
2. Allow installation from your browser or file manager if Android asks.
3. Open the app, add a model file, and start chatting.

> **Updating:** if you already have v0.14.2 or newer, this installs straight on top and keeps your chats. Coming from anything older than v0.14.2, uninstall once first — the signing key changed in that release.

## Verify what you downloaded

Every release lists the exact fingerprint of its installer so you can confirm the file is genuine and untampered before installing.

```
SHA-256:  23594d92df341b671dd8d0d8e60edf5f7d9a2ee9c211c0f2505c5b80c68d6989
```

On Windows PowerShell:

```powershell
Get-FileHash .\LLM-v0.22.0-public-arm64.apk -Algorithm SHA256
```

The value you get must match the one in the release notes exactly. If it does not, do not install the file.

## Features

### Private conversations
Natural, flowing chat with your own model, with saved history that stays on your device. Pick up any conversation where you left off.

### Characters and roleplay
Twenty-one characters are built in and ready the moment you open the app, in two collections.

**General** holds a senior engineer who answers with the fix rather than a lecture, a stage magician who will actually tell you how the trick is done, a diagnostician who troubleshoots anything broken, a curator who interviews you before recommending a thing, an emergency planner, a wilderness guide, and a night watchman who talks to the museum exhibits. **Cyberpunk** is the near-future set: privacy and threat modelling, forcing companies to delete your data, street medicine, salvage and repair, biohacking, conditioning, hardware builds, light-up clothing, invention, and security.

Several of them are not conversations but *procedures* — a typing engine that narrows sixteen personality types down to one, an interrogator who hunts for contradictions in your story, a machine that argues the strongest possible case against your plan, and a text escape room. Each shows its working as it goes.

Tap any card to start a chat where it greets you and stays in role. Import your own cards alongside them, kept in their own section so they never get lost among the built-ins. A set of ready-made behaviour presets lets you shape the assistant from strictly safe to completely unrestricted, and you can write your own.

### A workspace for code
A dedicated **Code** tab, next to Chat, built for programming rather than a chat with a coding prompt attached. The model answers in an unrestricted, get-it-done style and keeps writing across replies until the whole thing is finished. Organise your work into **projects**, link each project to a folder on your phone, browse that folder and load a file into your message, and let the model read and write the project's files itself. Everything the model produces is collected under **Files** to copy, save out, or keep as a reusable **snippet**, and code is coloured with proper **syntax highlighting** throughout. Ready-made quick-starts help you build a small tool you can actually use on the phone, work through a security task, or fix and understand existing code.

### Long answers, uninterrupted
When a reply is long, the app keeps it going on its own instead of stopping halfway — you get the whole answer without prompting for more.

### Fast on modern phones
On newer devices the app uses on-device acceleration to answer faster, and picks the right setting for each model automatically — no tuning required. Whether acceleration is available at all depends on the model file you bring; see [Which model file should I get?](#which-model-file-should-i-get) below.

### Made to read comfortably
A clean, modern interface with light and dark modes, adjustable text and spacing, high-contrast and reduced-motion options, and a range of accent colours to make it yours. Answers render properly — including tables — and a built-in Help section explains the options in plain language.

### Your own local API
Turn your phone into a private AI endpoint on your home network, so your other apps and devices can use your on-device assistant — still without touching the cloud.

### Safe by default
Optional app lock with PIN or fingerprint, encrypted backups, and a private-screen mode keep your conversations for your eyes only.

## Which model file should I get?

Your phone has two processors that can run a model, and which one your model gets to use is decided largely by the file you download — so it is worth thirty seconds before you pick one.

**The two processors, in plain terms:**

| | What it is | What it's good at |
|---|---|---|
| **CPU** | The general-purpose processor every phone has | Always works, with any model. The reliable default, and on most phones the fastest one too. |
| **GPU** | The graphics chip | Sometimes helps, sometimes doesn't — the app measures it once and then keeps the winner. |

**The one thing you control: the quantization.**

Model files come in "quantizations" — compression levels, written in the filename like `Q4_0` or `Q4_K_M`. This is not only a quality dial; it decides whether the GPU can run the file at all, because the graphics chip physically understands only certain formats.

- **`Q4_0` — the safe bet.** The format the GPU path accepts. If you want to give the GPU a chance, get this one.
- **`Q4_K_M`, `Q5_K_M`, `Q6_K`** — the most common downloads, marginally better quality, but **CPU-only**. If your model never leaves the CPU, this is almost always why.

Do not over-think it: the CPU path is well optimised (ARM KleidiAI, wide instruction support) and on many devices simply wins. A `Q4_K_M` model on the CPU is a perfectly good default.

**Curious what your model is actually using?** Settings → Device and performance names the exact reason for the model you have selected.

## System requirements

- A modern Android phone with enough memory and storage for the model file you intend to run.
- A compatible model file (which you provide) — see [Which model file should I get?](#which-model-file-should-i-get) if you want on-device acceleration.
- No internet connection required.

## License

Proprietary. All rights reserved. This repository contains the app's public documentation and releases only; the source code is not open.

© eVersor-HN
