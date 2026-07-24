# LLM v0.22.1

A private, on-device AI chat for Android. You bring the model file; everything runs on your phone.

A quick fix on top of v0.22.0.

## Fixed

**Crash on first start with a very large streaming model.** In v0.22.0, on phones with aggressive
memory management, loading a model much larger than RAM — then starting a new RPG — could get the app
killed by the system while it loaded or prepared the first scene. It was worst on a cold first start.

The app now caches experts more conservatively, especially on that first load before it has learned
what your device can handle, so it stays comfortably within budget and doesn't get killed. Verified
on-device on a 24 GB phone running a ~24 GB model: memory use dropped by about 6 GB and the app is
stable through loading and a heavy first scene.

If you installed v0.22.0, this updates straight over it and keeps your chats.

## Install

Download `LLM-v0.22.1-public-arm64.apk`, verify its SHA-256 against `SHA256SUMS.txt`, and install. The
build is signed with the project's release key, so it updates in place over an earlier install.
