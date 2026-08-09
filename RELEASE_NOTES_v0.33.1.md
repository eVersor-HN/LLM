# LLM v0.33.1

**Verify your download**

```
SHA-256:  2190ed3b7cd3579f809b89ea166ca476beee5db77fc3df496be4194083f9a510
```

```powershell
Get-FileHash .\LLM-v0.33.1-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

A model card described a model that was not the one running.

A Mixture-of-Experts model only streams its experts from storage when it does not comfortably fit in
memory. One that fits is loaded whole, because that is faster. The library was asking the wider
question — whether the model's *architecture* is capable of streaming — and so a 7 GB model that fits
easily was captioned "streams experts · needs ~13.6 GB free" while the app was in fact loading it
resident and using about 9 GB.

Two things were wrong with that. The card told you something untrue about what you were running, and
the check that decides whether a model may load at all was sized against the streaming figure instead
of the real one.

The condition now lives in a single place, next to the loader's own decision, and both the library and
the loader ask it. That matters more than the fix: this is the third bug of exactly the same shape —
the model-name test disagreeing with the recipe registry, a vision projector paired by guesswork, and
now "could stream" against "will stream". Each time the two answers had been written separately and
drifted. One answer, asked twice, cannot.

Everything else is v0.33.0; if you have not read those notes, they are worth a look — downloading a
model from a link, using a GGUF where it already lies without copying it, and dictation that stays on
the device.
