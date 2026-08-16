# LLM v0.36.0

**Verify your download**

```
SHA-256:  69f2606d5954bb4d03db433583b147ce1dcd5cdb54d3c0a08f33d3a6e4f9f703
```

```powershell
Get-FileHash .\LLM-v0.36.0-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

> 💸 Asking the model one yes-or-no question was costing you the whole conversation, every time. Tip if you got the minute back:
> **Ko-fi:** ko-fi.com/eversorhn
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

This release is mostly about the app telling you the truth, and one long wait that turned out to be
avoidable.

**A chat with web search on is dramatically faster.** Before answering in such a chat, the app asks
the model a short question of its own: does this need looking up? Asking it was throwing the
conversation away, so every single answer was preceded by the app re-reading the entire chat from the
beginning — around forty-five seconds of it, on a long conversation, purely to ask one yes-or-no
question. It no longer does. On the test conversation, the work that had to be redone before each
answer fell by roughly seven eighths.

**The model cards describe the file you are looking at.** A vision model's note claimed this app was
text-only and could not use the image half of it, which has not been true since v0.29.0. An
eighteen-megabyte file called "llama" was presented like any other model, with the confident
description of the family whose name it borrowed; the app now weighs the file against that claim, and
a file far too small to be what its name says is called what it is instead. A model that is currently
running no longer warns you that it needs more memory than you have free — it is running, so plainly
it does not.

**The web-search switch says what it actually does.** "Web search: on" read like a capability the
model might use. It is not: while it is on, every message in that chat is looked up before it is
answered, because a model cannot know what it does not know. That is deliberate and it stays — but
now the switch says so, and says that it stays on until you turn it off.

**Starting an adventure shows progress.** Opening a new story is the longest wait in the app, some
three minutes, and it offered a single unchanging line at the bottom of an empty screen while an
ordinary chat — which waits a fraction as long — showed a real percentage. It still shows no numbers
and no machinery, but the line now moves through the wait and a thin rule fills as the work is
actually done.

**A vision model and its add-on file are no longer identical rows.** They are named almost the same
by whoever published them, and at list width the two titles came out the same, so which one you were
about to load was not on the screen. The add-on is now drawn as what it is: indented under, and
dimmed.

**Photos in a chat no longer stutter the list.** They were being prepared at the very moment they
scrolled into view, which held the scroll up for as long as that took, and they were not kept
afterwards either — so scrolling back past the same photo paid the cost again. Both fixed.

**Chats in Chinese, Japanese and Korean stop breaking early.** The app estimates how much of the
model's context a conversation is using, and that estimate was written for European text — it
undercounted these scripts roughly threefold, so such a chat would hit a hard limit and produce no
answer at about a third of the length a German one manages.

**The RAM button also hands back the browser engine.** A single web search built one and it was then
held for as long as the app was open, for a feature you may have used once. Tens of megabytes, for
nothing.

**A gap in the private-network protection is closed.** Tools that fetch a page are not allowed to
reach addresses inside your own network. One whole family of those addresses — the kind a modern
router actually hands out internally — was not being checked, along with the range mobile carriers
place subscribers in. Both are blocked now.

**Backup import is honest about what it does.** It said it merges, which reads as though it works out
what you already have. It does not: importing the same backup twice gives you a second copy of
everything in it, and it now says so before you tap.
