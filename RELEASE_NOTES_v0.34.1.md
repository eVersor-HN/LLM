# LLM v0.34.1

**Verify your download**

```
SHA-256:  a1fb20dea52e76858035dd5bafd99533816d6f23838306f772995a4092c62b0a
```

```powershell
Get-FileHash .\LLM-v0.34.1-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

> 💸 Your model's private notes-to-self were being printed as part of its answers. They are not any more. Tip if it earned it:
> **Ko-fi:** ko-fi.com/eversorhn
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`

---

The labels v0.34.0 added were right and there were too many of them at once.

A model in the list now shows its name and only what decides whether you would look closer: whether
it is running, whether it can do something the others cannot, whether it will fit, how big it is.
Tap it and the rest appears — the remaining labels, what the model is good at, and a button to use
it. Five models with all their detail on screen at the same time was a wall, and a wall is not read.

**Tapping a model no longer loads it.** It used to, which meant brushing a 23 GB model while
scrolling started reading it from storage. Loading is something you ask for now, with a button that
says so.

## Also fixed

- **A model's notes to itself stopped appearing in its replies.** Some models think before they
  answer, and that thinking is meant to be folded away. One that stops and restarts its thinking was
  only having the first part removed, so the rest reached the chat — self-corrections, second
  thoughts, and a stray marker in the middle of the answer.
- **A greeting no longer triggers a web search.** With web search on, "hi" produced a request to
  research "Who am I?". It always asked permission first, which is precisely the problem: a prompt
  that appears every time you say hello teaches you to wave it through.
