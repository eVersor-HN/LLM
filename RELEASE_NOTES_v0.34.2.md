# LLM v0.34.2

**Verify your download**

```
SHA-256:  f145817b8bfe37754ac60d5cde9217f37e25c3c045227fe00cd5bd5ea308e675
```

```powershell
Get-FileHash .\LLM-v0.34.2-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

A quiet release. Nothing changes on screen.

The processor label removed in v0.34.0 left its machinery behind: every time the model list
refreshed, the app planned a load for each model in your library and looked up a saved benchmark
result to choose between "CPU" and "GPU" — for an answer that nothing displayed any more. Opening the
drawer now does that much less work.

Thermal throttling was also verified on real hardware for the first time. The behaviour is unchanged
and was already correct: when the phone is genuinely hot, a long reply stops at its length limit
instead of continuing itself, so the device is given a chance to cool rather than being pushed
further. It is now confirmed rather than assumed.
