# LLM v0.33.0

**Verify your download**

```
SHA-256:  339821d511c32b665d957c74b304c49d02de5a23ea670e01b129109c8dfaa6d2
```

```powershell
Get-FileHash .\LLM-v0.33.0-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

Getting a model onto your phone stops being the hardest part of using this app, dictation can now
stay on the device, and the app no longer tells you a percentage it does not know.

## A model in one move instead of three

Until now every model arrived the same way: find it in a browser, download it, then import it — and
the import makes a copy, so a 23 GB model wanted 46 GB of free space and a second long wait after
the first one. Both halves of that are gone.

**Download it here.** Drawer → GGUF → *From a link*, paste the address of the `.gguf` file, and it
lands directly in the app's own storage. Nothing to import afterwards, no browser download left over
to delete. If the connection drops, what arrived is kept — paste the same link again and it carries
on from there rather than starting over.

**Or do not copy it at all.** Picking a file from the phone now asks how you want it added. *Import a
copy* behaves as before. *Use where it is* keeps the file exactly where you put it and only remembers
permission to read it: a 23 GB model then costs 23 GB instead of 46, and appears in the library at
once instead of after a long copy. The trade is that the file has to stay put — move, rename or
delete it and the model says precisely that — and reading it through shared storage is a little
slower than from the app's own directory. Deleting a linked model from the library never touches
your file; it only gives back the permission.

## Dictation without leaving the phone

Speech recognition belongs to Android, not to this app, and on most phones it has meant sending what
you say to a service. Android 12 and newer also offer a recogniser that runs entirely on the device,
and the app now asks for that one first. Where it exists, dictation is as offline as everything else
here.

Where it does not, the ordinary recogniser still works — and the entry in the “+” menu tells you
which one you have: *Dictate a message (on this device)* or *(uses a speech service)*. In an app
whose whole point is that nothing leaves your phone, that is not a difference to leave unmentioned.

## The number while a reply is written

The percentage under a streaming reply meant two different things one after the other: how much of
your conversation had been read, and then how much of the length limit the answer had used. So it
climbed towards 100 %, and the moment the first word appeared it dropped back to nearly nothing —
twice per turn when a long answer continued itself.

It now measures one thing, and only while that thing is happening: *“reading the conversation ·
42 %”*. Once the model starts writing, a token counter takes over. It only ever goes up, which is
the honest form of “this is alive and it has got this far” — the length limit is a ceiling, not a
target, so no percentage of it would have meant anything. The counter earns its place most when
there is nothing to read on screen at all: a model that thinks before it answers can be busy for a
minute behind a hidden block.

## Adventures stop re-reading themselves

Every round of an adventure was re-reading the entire story before it could continue it. The turns
you play are deliberately invisible — an adventure should read as a tale, not as a chat log — and
they were being handed to the model and then thrown away, so the next round's history no longer
contained them. The cached context diverged at your previous move, and everything after it, the whole
last game-master reply included, had to be read again. Those turns are kept now, still invisible, and
the per-round material is frozen onto the turn it belongs to.

## Memory pressure, noticed while you are looking

Current Android versions stopped delivering the "running low on memory" signals to an app that is in
the foreground. The app was still listening for them, so the one lever it has — shrinking a streaming
model's expert cache — was only ever pulled after you had left the app, never during the long reply
that caused the pressure. It measures directly now, against the threshold your own device kills
apps at, and says so when it acts.

## Also fixed

- Restoring a backup no longer clears settings the backup never contained: a self-hosted SearXNG
  address and the two network switches were reset although they are deliberately not exported.
- Long menus open beside the button they belong to instead of a screen away.
- Two dialogs stopped cutting off their own explanation at the right edge.
- The composer's buttons grow with the accessibility text size instead of sitting small and low.
- A very small model is no longer captioned as a vision add-on.
- Dictation, clipboard and lifecycle use current Android APIs; the build has no deprecation warnings.
- The app declares itself as a game to the system. That is how phone makers gate their CPU and
  thermal boost paths, and it is worth real clock speed on a long generation.
