# LLM v0.33.2

**Verify your download**

```
SHA-256:  75baafb257073a17a2aea5e216a46cfeea68ef8bc8faba0264aec3052913d41c
```

```powershell
Get-FileHash .\LLM-v0.33.2-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

You bring your own model files, and the card in the library is the only place the app tells you what
you have. This release went through every claim on that card and fixed the ones that were not true.

## What your model is actually doing

The speed badge was the worst offender. It decided "⚡ CPU + KleidiAI · Q4_0 fast path" from the
quantisation and a four-gigabyte size limit — a rule the engine itself removed long ago as wrong in
both directions. Those fast ARM kernels come from a weight conversion the engine performs only when
there is memory to spare for it, and every k-quant benefits from it, not only Q4_0. So a small Q4_0
on a busy phone was promised a fast path it never got, while a 6.9 GB Q4_K_M running on exactly those
kernels was filed under "large". The engine now reports what it did and the badge simply repeats it.

A model running on the NPU was badged "CPU" — the one line in the app that says where the work
happens, naming the wrong processor. And the app said the NPU was "used automatically", which it
never was: Automatic always resolves to a processor profile that cannot select it. Both places now
say what to choose, and why you might not want to (the NPU reads long prompts far faster and writes
more slowly).

A model whose experts stream from storage was refused against a memory figure the engine never uses —
the app treated a ceiling as a requirement, while the engine sizes that cache to the phone it finds.
On a device with modest free memory, models that would have run were turned away. The figure in the
model list was also computed for a different configuration than the one that loads, quoting hundreds
of megabytes too much.

## Fixed

- A model used **in place** rather than copied was pinned to the CPU forever: the benchmark that
  chooses between processors was handed the file's location instead of its contents, failed, and
  cached the failure as a decision.
- **Downloads could not resume**, despite the app saying they could. Each attempt started over, and
  the abandoned part became invisible — to the library, to delete, and to you. An interrupted
  download of the same file is picked up now, and a dropped connection continues from where it
  stopped rather than throwing the gigabytes away. A server that answers a resume request with the
  whole file can no longer corrupt the result.
- Expert streaming is no longer announced for a model that will not stream, and the "force
  streaming" switch is no longer invisible to the check that could refuse the very model it was
  turned on for.
- The drawer is readable at the largest text sizes: the header buttons were being broken mid-word
  and the three counters ran into one another.
- The memory watchdog can be seen to have run. Release builds strip every log this app writes, so
  the one mechanism watching for a rare condition had no way to show it had measured anything. Its
  readings now appear in the diagnostics report.
