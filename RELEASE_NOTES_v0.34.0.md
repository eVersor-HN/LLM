# LLM v0.34.0

**Verify your download**

```
SHA-256:  13184b86ba335f709402be54460bb961863ef1a97f1e7731d4b48ad6a51275cf
```

```powershell
Get-FileHash .\LLM-v0.34.0-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

## Every model tells you what it is

A GGUF file is a name and a number of gigabytes. Everything else about it — whether it can look at a
picture, whether it will fit, what its weights are quantised to, whether it is one of the models that
can run from storage even though it is larger than your memory — you had to know already, or find out
by trying.

Each model in the library now carries a row of labels that says it.

The labels come in four weights, and the weight is part of the meaning. A **filled** label appears on
exactly one model: the one that is loaded, saying which processor it is actually running on. An
**outlined accent** label is an ability another model may not have — *Vision*, or *MoE · runs from
storage*. A **quiet outlined** label is a plain property: the size, the weight format, whether the
file is linked rather than copied. A **warning** label means the model will not load as things stand,
and says how much memory it wants.

Colour is never the only signal. Every label says its meaning in words, so the row still reads
correctly with the colour-vision setting on, or in a screenshot, or to someone who has never seen the
app before.

The processor label that used to sit on *every* card is gone. It said "CPU" or "GPU" in the shape of a
fact while guessing at a decision that had not been taken yet. Now only the loaded model is labelled,
and that label is the engine's own answer.

## Fixed

- **A loaded model no longer mislabels itself.** Once loaded, a 6.9 GB model announced that it runs
  from storage — because the library was measuring it against the free memory that the model itself
  was occupying.
- **A backup carries the whole of an adventure.** Restored stories kept their invisible turns but lost
  the record of what the game master had actually been told on each one.
