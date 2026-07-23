# LLM v0.21.0

A private, on-device AI chat for Android. You bring the model file; everything runs on your phone.

The big one: **run a model that is larger than your phone's RAM.** A Mixture-of-Experts model can now
stream its experts from storage as it writes, so a 25–30 GB model runs on a phone that could never
hold it all in memory — fully offline, nothing leaving the device.

## Highlights

**Models bigger than your RAM.** Mixture-of-Experts models (like Qwen3-30B-A3B) only use a small slice
of their weights for each word. LLM now keeps the shared parts in memory and reads each word's experts
from storage on demand, so a model far larger than your free RAM loads and runs on-device. It turns on
by itself, only when a model won't otherwise fit — everything smaller loads exactly as before.

**Tuned to stay alive on the phone.** Streaming is capped so the system's memory manager doesn't kill
the app mid-run, overlaps reading-from-storage with computing for speed, and the load screen no longer
tries to pull the whole file into memory at once. On a 24 GB phone a 25 GB model runs at a usable pace.

**Also new since the last public build:**

- **Adventure mode.** A third tab turns the app into a text-adventure game master — roll a d20 by
  shaking the phone, watch dice that look thrown, a character sheet that fills in as you play, and the
  drawer becomes a chronicle of your story.
- **Dictation in the composer** — speak your message instead of typing it.
- **A Code tab** (from v0.18.0) — a private coding workspace with projects, files, and syntax
  highlighting.

## Notes

- The MoE streaming feature needs a Mixture-of-Experts GGUF and enough free storage for it. Loading is
  slower than a model that fits in RAM (it reads from flash every word), and reads storage heavily.
- CPU/GPU build; no Qualcomm NPU content.

## Install

Download `LLM-v0.21.0-public-arm64.apk`, verify its SHA-256 against `SHA256SUMS.txt`, and install. The
build is signed with the project's release key, so it updates in place over an earlier install.
