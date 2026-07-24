# LLM v0.22.0

A private, on-device AI chat for Android. You bring the model file; everything runs on your phone.

This release makes streaming a model that's larger than your RAM smarter and more stable, cleans up the
message bar, and fixes a few things about how the Chat / Code / RPG tabs behave.

## Highlights

**Streaming that tunes itself to your phone.** When a model streams its experts from storage (because
it's too big to hold in RAM), the app now learns how much memory to cache — per device and per model —
and remembers it for next time. It watches for the tell-tale sign that the cache is stealing memory the
model itself needs, and backs off before that turns into a slowdown or a crash. It also shrinks the
cache on the fly when Android reports memory pressure or the phone gets hot, then restores it for the
next reply. The upshot: big models stay alive and usable instead of getting killed mid-run.

**Optional: stream even when it fits.** A new *Force MoE expert streaming* switch (Settings → Device &
performance) lets you stream a Mixture-of-Experts model's experts from storage even when it would fit in
RAM — trading a little speed for a much smaller memory footprint. Off by default. A small status line
shows when a model is streaming and how it's been tuned.

**A cleaner message bar.** Attach, dictate, and web-search now live in a single "+" menu instead of
crowding the text field, so the field is much wider. The old emoji symbols are gone — the composer's
icons are now hand-drawn to match the rest of the app.

## Changed

- The **Adventure tab is now called RPG**.

## Fixed

- **A reply could show up in more than one tab at once.** The live, streaming text now stays in the tab
  where you started it, instead of following you when you switch tabs mid-reply.
- **Typing a first message on the Code tab** now opens a real code session that stays in the Code tab,
  instead of quietly starting an ordinary chat.

## Notes

- Streaming a model bigger than your RAM needs a Mixture-of-Experts GGUF and enough free storage. It's
  slower than a model that fits in memory (it reads from storage for every word) and reads storage
  heavily. Streaming turns on by itself only when a model won't otherwise fit — everything smaller
  loads exactly as before.
- The self-tuning settles over a few real runs on your device; the first run or two are it feeling out
  your phone.
- CPU/GPU build; no Qualcomm NPU content.

## Install

Download `LLM-v0.22.0-public-arm64.apk`, verify its SHA-256 against `SHA256SUMS.txt`, and install. The
build is signed with the project's release key, so it updates in place over an earlier install.
