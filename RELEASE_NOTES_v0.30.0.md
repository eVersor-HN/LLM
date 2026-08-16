# LLM v0.30.0

**Verify your download**

```
SHA-256:  c6c0504ce7bc5626273de7bccff638f5f9abcad50a42506385184c7733a5d76d
```

```powershell
Get-FileHash .\LLM-v0.30.0-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

> 💸 The model can look things up on the web now, and replies got faster the longer you talk. Tip if it earned one:
> **Ko-fi:** ko-fi.com/eversorhn
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

## Web search that actually searches

- **Ask about something current and the model looks it up.** Turn on “Web search” in the + menu and
  it now searches before it answers — versions, prices, news, who currently holds an office —
  instead of answering from a memory that stops at its training date. Until now it simply ignored the
  ability: told the protocol, told to search, even shown a complete worked example, it still answered
  from memory every time. Asked who the economics minister is, it named the previous one, and nothing
  about the answer looked wrong.
- **“Research” does the whole lookup in one step.** One request runs several searches at once, opens
  the most promising results in parallel, splits them into passages, ranks those against your
  question and hands the model a short numbered set of sources. The alternative — search, then open a
  page, then open another — costs a full pass over the conversation per step, which on a phone is by
  far the slowest part.
- **Answers cite what they read.** Sources are numbered and the reply points at them: “…elected with
  325 votes [4]”, where [4] is the page that says so.
- **A lookup is a card, not a wall of text.** The tool that ran, a one-line summary and the sources it
  used, with the passages folded away behind an arrow — tap to read them and check a claim yourself,
  tap a source to copy its address. A failed lookup is marked in red and says why.
- **The crawler follows the trail on purpose.** Give it a starting page and something to look for and
  it visits the most relevant links first instead of whatever the site happens to list first, with
  three breadths to choose from — a few pages, one site, or off across the web on mains power.
- **Self-hosted search now works at all.** A private SearXNG on your own machine or phone was
  unreachable no matter how it was configured, because Android refuses plain HTTP. Help gained a
  section on what SearXNG is, how to run one, and the two settings that decide whether it works.

## Replies get faster the longer you talk

- **Each turn no longer re-reads the whole conversation.** The app was rebuilding the model's entire
  context from scratch on every single message. Now it keeps what it already has: measured on a
  four-turn chat, 914 of 1002 tokens reused and 88 processed instead of 1002. A two-turn exchange went
  from 23 to 12 seconds, and the saving grows the longer the conversation gets.

## Fixed

- **A tool request written by the model was thrown away** unless the reply happened to be nothing but
  the request itself — so a model that wrote one polite sentence first was ignored.
- **A vision add-on was attached to models it cannot belong to.** With one projector in the library it
  was paired with anything, and the failure only flashed by in the status line. It now refuses a
  pairing the files themselves disprove, explains it, and says when a pairing was made purely by
  elimination.
- **A research result could be too large to answer.** It was capped at a fixed size regardless of how
  much room the conversation had left, so a perfect set of sources arrived and the reply never came.
  It is now sized against the space that is actually free.
- The Adventure tab's opening screen had **no way to start an adventure** — only the monogram, with
  the sole entry point hidden behind an edge swipe.

---

**Build:** arm64-v8a, CPU backend, signed.
Everything still runs on your device. Web search is off unless you turn it on, and then only your
query goes to the search provider you configured.
