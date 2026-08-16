# LLM v0.31.0

**Verify your download**

```
SHA-256:  3407b4a6d3f8d6c7804fecc8cafe05f1f9a350fb147fd866cdb452c176f8b564
```

```powershell
Get-FileHash .\LLM-v0.31.0-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

> 💸 Every free search server on the internet stopped talking to me, so the app grew a browser. Tip if it earned it:
> **Ko-fi:** ko-fi.com/eversorhn
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

Web search works on a phone that was just installed, with nothing set up first.

## Search no longer needs anything set up first

Until this version the app asked public SearXNG servers for machine-readable results. Every one of
them has stopped answering: three rate-limit anything that is not a person, two reply with a
“verifying you are human” page, one is gone. A freshly installed app therefore could not search at
all, and the only remedy on offer was to type in the address of a search server you host yourself —
which presumes both that you host one and that you know its address.

Search now runs through the browser engine Android already has on it. The app opens an ordinary
results page out of sight, reads the results off it and closes it again. Nothing to configure, no
account, no API key.

**When a page asks whether you are a person, it asks you.** The check appears in the app, on the page
that wants it, and you answer it yourself. The app does not solve these for you — it could, but that
would be pretending to be something it is not, on someone else's server, and it would break the next
time the puzzle changed. The answer is remembered for a while, so it does not come back every time.

**What it costs, plainly.** The search page is loaded in full, including whatever scripts and cookies
it brings, exactly as it would be in your normal browser. Third-party cookies are refused and images
are not downloaded, but the search engine sees your query and an ordinary browser's fingerprint.
Nothing else changes: the model still runs entirely on your device, and nothing leaves it unless you
switch web search on.

**A SearXNG of your own is still better** — it answers with plain data instead of a web page, so it is
faster and lighter, it never asks whether you are a person, and the query never leaves hardware you
own. It is now a choice for people who want it rather than the price of entry.
Settings → Tools → Search provider.

## Fixed

- **“Web search” switched on everything except the crawler.** The toggle in the + menu forced on
  search, page fetch and research, but left the crawler at a global setting that is off by default —
  so the one tool that can follow a trail was silently missing, and its absence was the only clue.
- **A local address now says why it cannot work.** Pinning `http://127.0.0.1:8888` reaches a computer
  on your desk only while the phone is plugged into it; away from the desk the failure read as a bare
  “connection failed”, with nothing to suggest the address itself was the problem.

## Help

Two new entries explain how search works now, what the browser engine means for your privacy, and
what to do when a page asks you to confirm you are a person.

## Install

1. Download `LLM-v0.31.0-public-arm64.apk`.
2. Check the SHA-256 above.
3. Install. Existing chats, models and settings are kept.

Requires arm64 Android 6.0 or newer.
