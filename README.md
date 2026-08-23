# LLM

**Local capability. Direct control. No account, no cloud, no telemetry.**

A complete AI chat that runs entirely on your Android phone. You bring the model file; the app does
the rest — offline, private, and yours. Built for people who want a modern assistant without handing
their words to someone else's computer.

Airplane mode works perfectly. Out of the box the app makes no network connection at all.

---

## Product status

**Closed-source, proprietary software.** This repository carries the public documentation and the
official releases. The source code is not published and no open-source rights are granted. See
[LICENSE](LICENSE).

---

## Support the project

It runs offline so nobody can bill you — which is exactly why nobody bills me. Tip if it earned it.

- **Ko-fi** — https://ko-fi.com/eversorhn
- **PayPal** — https://paypal.me/FAMarco
- **Bitcoin** — `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

## Local first, private by design

- **Offline by default.** No network connection at all unless you switch on one of the two optional
  online features below.
- **No account, ever.** Nothing to register, nothing to log in to, no profile to build.
- **No telemetry.** No analytics, no crash reporting, no phone-home — not even an optional one.
- **Data stays local.** Chats, characters, imported files and settings live in local app storage,
  encrypted at rest.
- **No lock-in.** Export your data whenever you want and take it with you.

### What can talk to the internet

Two features can send data off the device. **Both are off by default** and each takes deliberate
steps to switch on. Full detail in [SECURITY.md](SECURITY.md).

- **Web search, open webpage, crawl.** Sends your query text, or the URL you asked to open, to the
  provider you configured. Chat history and system prompt are never sent. Every request is shown to
  you for approval before it runs.
- **Local API server.** An optional endpoint for your other apps on your own network. Loopback-only
  unless you enable LAN mode, and always behind a generated bearer token.

If you never enable either, the app never opens a socket.

---

## Official distribution

Author: **eVersor-HN**
Official repository: **https://github.com/eVersor-HN/LLM**

Official binaries come only from the [Releases](../../releases) page of this repository. A file
obtained anywhere else is not an official binary, whatever it is called.

## Download and install

1. Download the latest `.apk` from [Releases](../../releases).
2. Verify its SHA-256 (below).
3. Allow installation from your browser or file manager if Android asks.
4. Open the app, add a model file, and start.

> **Updating:** v0.14.2 or newer installs straight on top and keeps your chats. Coming from anything
> older, uninstall once first — the signing key changed in that release.

## Verify authenticity — SHA-256

Every official binary is published with its SHA-256 in the corresponding GitHub Release. **The
filename and the hash must both match exactly.** If either does not, do not install the file.

```
LLM-v0.37.0-public-arm64.apk
c02ad051249680022e9087dd5cbace1f573c8ab490ef17dcd81882225b03513d
```

Windows PowerShell:

```powershell
Get-FileHash .\LLM-v0.37.0-public-arm64.apk -Algorithm SHA256
```

---

## Features

### Control
- Runs entirely on your own hardware, on a model file you choose.
- No forced account, no mandatory cloud, no external dependency for normal use.
- Optional app lock (PIN or fingerprint), encrypted backups, private-screen mode.

### Conversation
Natural, flowing chat with saved history that stays on your device. Long answers keep going on their
own instead of stopping halfway. Answers render properly, tables included.

### Twenty-one built-in characters
Ready the moment you open the app, in two collections. **General** holds a senior engineer who
answers with the fix rather than a lecture, a stage magician who will actually tell you how the
trick is done, a diagnostician, a curator who interviews you before recommending anything, an
emergency planner, a wilderness guide, and a night watchman who talks to the museum exhibits.
**Cyberpunk** is the near-future set: privacy and threat modelling, data deletion, street medicine,
salvage and repair, biohacking, conditioning, hardware builds, light-up clothing, invention and
security.

Several are not conversations but *procedures* — a typing engine that narrows sixteen personality
types down to one, an interrogator who hunts contradictions in your story, a machine that argues the
strongest case against your plan, and a text escape room. Each shows its working as it goes.

Import your own cards alongside them, kept in their own section. Behaviour presets run from strictly
safe to completely unrestricted, and you can write your own.

### Text adventures
A built-in RPG mode turns the model into your game master, with a live character sheet: health,
attributes, inventory and status, kept current as the story unfolds. No menu of options — you write
what you do, in your own words. When what you try could fail, a physical die falls across the screen
and decides it; shake the phone while it is in the air and it keeps tumbling until you let it drop.
Keep world notes for the places, people and secrets that matter, and the game master stays
consistent with them.

### Models far larger than your memory
Some of the strongest models available are far bigger than any phone's memory. This app runs them
anyway, reading the parts it needs from storage as it goes — a 24 GB model on a phone with nowhere
near 24 GB free is an ordinary Tuesday here. See [Which model should I get?](#which-model-should-i-get)
for which families this applies to.

### Nothing loads by surprise
Every model states how much free memory it will actually need before you tap it, and the drawer
shows how much your phone has, live. If something is loaded and you want the memory back, one button
hands it over.

### Vision and documents
Models that can see accept photos. PDF, Word, Excel and plain text are read into the conversation,
and you see the extracted text before anything is sent.

### Voice
Dictate instead of typing, on-device on Android 12 and newer. Replies can be read aloud.

### Made to read comfortably
Light and dark, adjustable text and spacing, high-contrast and reduced-motion options, a range of
accent colours, and a Help section written in plain language.

### Your own local endpoint
Turn your phone into a private AI endpoint on your home network, so your other devices can use your
on-device assistant — still without touching the cloud.

---

## Which model should I get?

**Start with a Mixture-of-Experts (MoE) model.** They are the reason this app can run something
bigger than your phone's memory: only the parts needed for the current word are read from storage,
so a model several times your free memory still runs.

That works for these families:

- **Qwen3 MoE** and **Qwen2 MoE** — e.g. Qwen3-30B-A3B
- **Qwen3-VL / Qwen2-VL MoE** — the same, with images
- **Qwen3.5 MoE** — e.g. 35B-A3B
- **Gemma 4 MoE** — e.g. 26B-A4B
- **gpt-oss** — 20B and 120B
- **LFM2 / LFM2.5 MoE** — e.g. 8B-A1B, 24B-A2B

Everything else — ordinary dense models, and MoE builds outside that list such as Mixtral or
DeepSeek MoE — has to fit in your free memory. It will still load if it does not, but a dense model
needs all of its weights for every single word, so expect many seconds per word.

**A safe first model:** Qwen3-30B-A3B in a Q4 quantization. Good German and English, and it streams.

### About quantization

Model files come in "quantizations" — compression levels written into the filename like `Q4_0` or
`Q4_K_M`. It is not only a quality dial: it decides whether your phone's graphics chip can run the
file at all.

- **`Q4_0`** — the format the GPU path accepts. Take this one if you want to give the GPU a chance.
- **`Q4_K_M`, `Q5_K_M`, `Q6_K`** — the most common downloads, marginally better quality, CPU-only.

Do not over-think it. The CPU path is well optimised and on many devices simply wins; a `Q4_K_M`
model on the CPU is a perfectly good default. Settings → Device and performance names the exact
reason for the model you have selected.

---

## Limitations and known boundaries

- **The model writes the answers, not the app.** Output can be confidently wrong. See
  [DISCLAIMER.md](DISCLAIMER.md).
- **No model is included.** You supply the file.
- **Speed depends on your device and the file.** A model much larger than your memory runs at a
  calm pace and reads heavily from storage.
- **LAN mode of the local API server is plain HTTP.** Use it only on a network you trust.
- **DNS rebinding is not defeated** by the address filter that protects the web tools; see
  [SECURITY.md](SECURITY.md) for why.
- **A rooted or compromised device defeats the app's protections.** The app lock raises the bar; it
  does not replace device encryption and a screen lock.

## System requirements

- Android phone, **arm64**.
- Enough free memory and storage for the model file you intend to run — the app tells you how much
  before you load it.
- A model file in GGUF format, which you supply.
- No internet connection required.

---

## License

**Proprietary. All rights reserved.** You receive a limited, personal right to use the distributed
application. Redistribution, modification and reverse engineering are not permitted. Third-party
components remain governed by their own licenses — see [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md).
The authoritative text is [LICENSE](LICENSE).

Full version history: [CHANGELOG.md](CHANGELOG.md)

© eVersor-HN
