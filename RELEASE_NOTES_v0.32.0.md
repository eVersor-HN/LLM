# LLM v0.32.0

**Verify your download**

```
SHA-256:  bf7641ba1c2581f52ad06eb753d91583a33fc170360970342eb103d9ebaeb4d1
```

```powershell
Get-FileHash .\LLM-v0.32.0-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

Vision models find their projector, huge Qwen3-VL models stream their experts again, and the app
stops claiming things it has not checked.

## Vision models find their projector

A vision model is two files: the model itself and a projector that turns pixels into something it
can read. Matching the two was done by the names stored *inside* the files — and a converter is free
to leave those as the base model's, or blank. The Qwen3-VL projector ships as a bare
`mmproj-F16.gguf`, which scored zero against the very model it was exported for. File names, which
publishers do keep in step, are now compared as well.

That alone was not enough. Everything a publisher ships carries their handle and the family in
front, so `Huihui-Qwen3-30B-A3B-…` and `mmproj-Huihui-Qwen3-VL-8B-…` share twenty-two characters
without being related at all — enough to label a text-only 30B model *Vision*. A parameter count
that both names state and that disagrees, `30b` against `8b`, now settles it, and no amount of
shared prefix outvotes that.

And when the projector simply is not there, the app says so. Before, that card looked exactly like a
text-only model's: the file is present, it chats normally, and the only symptom is a *Vision* label
that never appears. It now names the file to look for.

## Models bigger than your memory

Qwen3-VL MoE models stream their experts again. The streaming engine had no recipe for this
architecture, so a 30 GB vision MoE quietly fell back to ordinary loading and thrashed — 83 seconds
to read a single image.

More importantly, the app no longer promises streaming it cannot deliver. Two places decided whether
a model streams and they disagreed: one asked whether the architecture name contains "moe", the
other asked the engine's list of supported ones. Anything that passed the first and failed the
second was admitted against the memory estimate for *streaming* and then loaded whole. Both now ask
the engine.

Help opens with this, because it is the thing a phone is not supposed to be able to do: how a 30 GB
model runs on 8 GB free, which model families can do it, and how to recognise one before you
download it.

## Fixed

- **A model could lock itself out of its own chat.** The memory check credited back the model being
  replaced — but only a *different* one. Re-selecting the model already loaded credited nothing, so
  a 23 GB model was measured against memory that this very model was occupying. The bigger the
  model, the more certain it was to happen.
- **"I can only see `<media>`."** The marker that tells the projector where an image goes is plain
  text. A model that echoes it leaves one behind for good, and every later turn then sent a marker
  with no image behind it — so the model correctly reported seeing a placeholder and nothing else.
- **Roughly 200 MB written to storage after every reply.** The conversation cache was saved for any
  chat longer than one message, but the file costs the whole cache allocation however little of it
  is used: one reply cost 182 MB to preserve a single token.
- **Web search worked out of the box everywhere except in the setting that decides it.** The default
  is the built-in browser, and the browser is the only path that can show a "confirm you are a
  person" page — but the settings loader handed out SearXNG to anyone who never opened Settings.
  Searches went to public servers that now answer with a rate limit, and no check could appear.
- A refused load no longer claims nothing is loaded; deleting a projector no longer leaves its model
  claiming *Vision*.

## Plainer words

Memory warnings dropped the vocabulary of the implementation. "Safe-load check blocked this
configuration: estimated peak 8.1 GB, safe budget 7.3 GB" described the machinery; it now says what
is too big, by how much, and which of your options changes it. The library says what a streamed
model costs, in words: file size is not the limit, but expect seconds per word.

## Removed

Five leftovers from features that were deliberately taken out and whose code stayed behind — the
prompt-mode switch, the active-card indicator, a drawer row for two sections that no longer exist,
the CPU/GPU badge, and the adventure re-roll that went when free-text play arrived. Eighty-nine
lines, none of them reachable.

---

**Updating:** installs straight on top of v0.14.2 or newer and keeps your chats.
