# LLM v0.35.0

**Verify your download**

```
SHA-256:  0fe7d7d391c50ee6b04485a8b29705b06b32ba7360ef892ffcd1d84b79209c0d
```

```powershell
Get-FileHash .\LLM-v0.35.0-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

> 💸 The button that promised to free memory spent three months freeing none of it. Tip if it earned it now:
> **Ko-fi:** ko-fi.com/eversorhn
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

This release is about memory: the models it stops you running, and the button that promised to help.

**Models larger than your free memory now run.** A model file bigger than the memory the phone had
spare was refused outright. That was the wrong question to ask of it — a model that large is not held
in memory all at once, it is read from storage as it is used, and its actual working set is a
fraction of the file. So it loads now, and its card leads with what that costs rather than burying
it: "slow · reads from storage", and expect many seconds per word. On a 24 GB phone with 16 GB free,
a 15.6 GB model that could not be opened at all now opens. It will be slow, and the app says so
before you start rather than after.

**There is now a RAM button in the top bar.** It unloads whatever model is resident, then asks
Android to take memory back from other apps, and reports the figure it measured rather than the one
it was aiming for. Background apps may be closed to pay for it — nothing of theirs is deleted, they
simply start fresh the next time you open them — so it always asks first, from either place you can
reach it.

**And that button now does what it says.** Its first version was so careful with the phone that it
never applied any real pressure: it backed off within a third of a second and handed everything
straight back, and measured against itself it gained nothing at all. The reading was right; the
conclusion drawn from it was not. It now keeps asking for as long as the phone can answer, and stops
where there is genuinely nothing left to give rather than at the first sign of effort. On a 24 GB
phone with fifteen apps sitting in the background it takes back about half a gigabyte where it
previously took back none — on top of whatever the unloaded model was holding, which for a 12B model
is another nine.
