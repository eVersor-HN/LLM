# LLM v0.14.4

A small follow-up to v0.14.3: the built-in characters now tell you what they are, and editing a message
happens where the message actually is.

## Changed

**The six built-in characters introduce themselves.** Each one shows a one-line description in the card
list instead of six identical "Tap to start a new chat" subtitles — so you can tell Ada from Vera from
MERIDIAN without opening them first.

## Fixed

- **Editing a message stayed put.** Long-pressing a message and choosing Edit used to open a plain
  system dialog in the middle of the screen, in styling that did not match the rest of the app and
  nowhere near the text you were editing. The message now opens up in place, keeps its position and the
  app's own look, and the text field is focused and ready the moment it appears.

---

**Verify your download**

```
SHA-256:  d04976df6e95fac7986310a1001c9a2023aa7e2278dbbfc4f713a96dcee03fbe
```

```powershell
Get-FileHash .\LLM-v0.14.4-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

**Updating:** coming from v0.14.2 or newer, this installs straight on top and keeps your chats. From
anything older, uninstall once first.

Full history: [CHANGELOG.md](CHANGELOG.md)

---

> 💸 This release exists because someone told me a dialog looked wrong. That is the entire business model:
> **PayPal:** paypal.me/FAMarco
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`
