# Changelog

All notable changes to LLM, newest first. Each version's installer and its SHA-256 fingerprint are on
the [Releases](../../releases) page.

## v0.17.0 — 2026-07-19

The first public release of the current line. Earlier builds are no longer distributed.

### Added

- **Twenty-one built-in characters** in two collections, *General* and *Cyberpunk*, with your own
  imported cards kept in a separate *Custom* section. Several of them are interactive procedures
  rather than conversations: a personality-typing engine, an interrogator who hunts for contradictions
  in your story, a machine that argues against your plan, and a text escape room. Each shows its
  reasoning as it narrows down.
- **A reply language setting** — Automatic, English, German, Spanish, French or Portuguese. This sets
  the language the model answers in; the app's own interface remains English.
- **Natural reply length**, now the default. It adds no length instruction at all, so the model answers
  the way it normally would, and long answers continue automatically instead of stopping short. Short,
  Medium and Long remain as deliberate limits.
- **A startup model setting** (Settings → Device and performance). "Last used" reopens whichever model
  you were on; pin one to always start with that model instead.
- **Full licence texts** for every bundled open-source component are now shipped inside the app and
  readable under Settings → About → Open-source licenses.

### Changed

- **Character cards now actually set the scene.** A card's opening message is part of the persona the
  model is given, so the introduction keeps working for the whole conversation instead of being
  forgotten once the chat grows. `{{char}}` and `{{user}}` placeholders are filled in.
- **A reply that runs into the length limit finishes its sentence** instead of stopping mid-word.
- **Stop keeps what was written.** Pressing Stop used to discard the entire reply; it is now saved, and
  Continue picks up exactly where it left off.
- **Model loading progress** moved into a compact dialog in the middle of the screen instead of a
  banner that pushed the conversation around.
- **The card list opens collapsed**, so the drawer is a choice rather than a scroll.
- **Deleting every chat now really leaves none** — the app greets you and your first message starts a
  new conversation.
- New app icon: a brain drawn as a circuit board.
- Models run on the CPU or, where it wins, the GPU. The app measures the GPU once and keeps whichever
  came out ahead.

### Fixed

- Backups no longer lose per-chat settings. Adventures, per-chat personas, reply lengths and retry
  variants survive an export/import cycle.
- Deleting a chat now removes everything belonging to it, including saved alternative replies.
- Long generations no longer stall when the screen is off.
- An imported character card can no longer break the app by being unusually large, and card text can no
  longer escape its own message to influence the app's instructions to the model.
- The app no longer crashes after long cumulative use on Android 15.
