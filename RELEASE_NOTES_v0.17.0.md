# LLM v0.17.0

A private, on-device AI chat for Android. You bring the model file; everything runs on your phone.

This is the first public release of the current line. Earlier builds have been withdrawn and are no
longer distributed.

## Highlights

**Twenty-one built-in characters.** *General* holds a senior engineer who answers with the fix rather
than a lecture, a stage magician who will actually tell you how the trick is done, a diagnostician for
anything broken, a curator who interviews you before recommending a thing, an emergency planner, a
wilderness guide, and a night watchman who talks to the museum exhibits. *Cyberpunk* is the near-future
set: privacy and threat modelling, forcing companies to delete your data, street medicine, salvage and
repair, biohacking, hardware builds, invention, and security. Your own imported cards sit in their own
*Custom* section.

**Some of them are procedures, not conversations.** A typing engine that narrows sixteen personality
types down to one, asking only questions that separate whoever is still standing. An interrogator who
keeps a record of your story and hunts for contradictions in it. A machine that argues the strongest
possible case against your plan and tells you honestly how it held up. A text escape room.

**Characters now hold their scene.** A card's opening message is part of the persona the model is
given, so the introduction keeps working for the whole conversation rather than being forgotten once
the chat grows longer.

**Replies end properly.** A reply that runs into the length limit finishes its sentence instead of
being cut mid-word. The new default length, *Natural*, adds no length instruction at all — the model
answers as it sees fit, and long answers continue on their own.

**Stop no longer throws your reply away.** Press Stop and what has been written is kept; Continue picks
up exactly where it left off.

**Choose the language of the replies.** Automatic, English, German, Spanish, French or Portuguese.
Automatic simply lets the model answer in the language you wrote in.

**Pick which model opens at startup** under Settings → Device and performance, instead of whichever one
the app happened to list first.

## Also fixed

- Backups keep per-chat settings — adventures, personas, reply lengths and alternative replies survive
  an export and import.
- Deleting a chat removes everything belonging to it.
- Long generations no longer stall while the screen is off.
- An unusually large character card can no longer break the app, and card text can no longer reach past
  its own message to influence the app's instructions to the model.
- No crash after long cumulative use on Android 15.

## Processors

Models run on the **CPU or the GPU**. The CPU path is well optimised — ARM KleidiAI and the full
instruction set of modern ARM chips — and on most phones it is the faster of the two. The app measures
the GPU once and then keeps whichever came out ahead, so there is nothing to configure.

## Privacy

The app makes no network connection at all unless you switch on one of two optional features — web
search or the local API server. Both are off by default and each takes several deliberate steps to
enable. There is no telemetry, no analytics and no account. See the README for exactly what each one
sends and to whom.

## Install

Download `LLM-v0.17.0-public-arm64.apk` below and open it on your phone. Android will ask you to allow
installation from this source. Requires arm64 Android 8.0 or newer.

Verify the download if you like:

```
sha256sum LLM-v0.17.0-public-arm64.apk
6068858aa79669a94805af423a6707772970273fe2ee83f168fbdb090e350a21
```

## Support

The app is free and runs offline, so nothing bills you — and nothing bills me either. If it earned it:

**PayPal** — paypal.me/FAMarco
**Bitcoin** — `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`
