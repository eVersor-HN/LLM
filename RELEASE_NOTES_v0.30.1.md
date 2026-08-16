# LLM v0.30.1

**Verify your download**

```
SHA-256:  484c547be1af25763525e3ff6444aa4387650b5bcfd653052c09966cf62d60e4
```

```powershell
Get-FileHash .\LLM-v0.30.1-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

> 💸 A check I added last week decided your vision model was not a vision model. Tip if you got it back:
> **Ko-fi:** ko-fi.com/eversorhn
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

A correction to 0.30.0. If you installed that version and use a vision model, please update.

## Fixed

- **A vision model was refused, and then permanently marked as text-only.** 0.30.0 added a check that
  compared the model's embedding size with the projector's and rejected the pair when they differed.
  A projector's file describes its own vision tower, not the size it feeds the language model with,
  so the two numbers were never comparable — and a working pair was turned away. Because the
  capability is recorded after a load, the model then stayed labelled text-only for good. If 0.30.0
  did that to one of your models, this version repairs the label on the next start; nothing needs to
  be re-imported.
- **A model now says it can see before it has ever been loaded.** Until now the “Vision” marker only
  appeared after the first successful load, so a freshly imported model and its projector looked
  text-only, with nothing to suggest that images would work. The library is read directly instead,
  in both directions — importing either half updates the other — and the marker is corrected in both
  directions too, so one written in error cannot outlive its cause.
- The About screen credits **eVersor-HN**.

Everything in [0.30.0](RELEASE_NOTES_v0.30.0.md) — web search, research, the crawler, and replies
that stop re-reading the whole conversation — is unchanged and included.

---

**Build:** arm64-v8a, CPU backend, signed.
Everything still runs on your device. Web search is off unless you turn it on, and then only your
query goes to the search provider you configured.
