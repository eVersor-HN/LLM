# LLM v0.30.2

**Verify your download**

```
SHA-256:  6a49cbb67e44bfd899a2aae826d063d85daac9cce67bc017e9c685802846f61d
```

```powershell
Get-FileHash .\LLM-v0.30.2-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

> 💸 This one is mostly the app admitting things it had quietly known all along. Tip if it earned it:
> **Ko-fi:** ko-fi.com/eversorhn
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

A small release. One thing the app never said out loud, and a set of fixes for text size, document
attachments and web lookups.

## Added

- **The model list says that a model does not have to fit in your memory.** It is the one thing
  about this app you cannot work out by looking at it: a Mixture-of-Experts model reads only the
  part it needs for the word it is writing, straight from storage, so one several times larger than
  your free memory still runs on the phone. Until now the only trace of that was a
  “streams experts · needs ~8.1 GB free” under a 30 GB file, which reads like a typo. A short note
  above the model list explains it, expands if you want the detail, and can be dismissed for good.

## Fixed

- **Dialogs ignored the text size you set.** Every screen followed the accessibility text slider
  except the dialogs — which is where the short, important sentences live: what a model failed at,
  what leaving now would discard. Measured at 159 %, a dialog title came out exactly the size it was
  at 100 %. It grows with the rest of the app now.
- **Long labels were cut in half instead of wrapping.** At large text sizes the drawer buttons, the
  free-memory line and the donation row clipped mid-word.
- **A lookup searched the wrong year.** The model cannot know today's date, so a question about
  something current was searched as though it were still the year the model was trained in. The date
  is part of what it is told now. A greeting is also allowed to be a greeting again — “hello” no
  longer sends anyone to the web.
- **The vision add-on warning interrupted every model load.** It appeared whenever a projector could
  not be paired, including for models that have nothing to do with images. It is raised where it
  matters — when a photo is actually refused — and clears itself when a pairing later succeeds.
- **A scanned PDF said the wrong thing.** Attaching one reported “no readable text was found”
  instead of suggesting a photo of the page, which a vision model can read. The pages of a scanned
  document are pictures, and pictures were not being counted — so the advice written for exactly
  that case could never appear.
- **Every RTF attachment began with its own font list.** Word processors write a font table, a
  colour table and a stylesheet before the first sentence, and all of it was handed to the model as
  if it were text (“Times New Roman;Arial;Normal;”). Braces written inside a document survive now
  too.

## Notes

- Every attachable document format — `.pdf`, `.docx`, `.xlsx`, `.pptx`, `.odt`, `.ods`, `.odp`,
  `.epub`, `.rtf` — is now covered by tests that build a real file of that format and read it back.
  That is how the two fixes above were found: extraction returning nothing looks exactly like a
  document that contains nothing.
- Thermal throttling, dictation and document attachments were re-verified on device for this
  release.

## Install

1. Download `LLM-v0.30.2-public-arm64.apk`.
2. Check the SHA-256 above.
3. Install. Existing chats, models and settings are kept.

Requires arm64 Android 6.0 or newer.
