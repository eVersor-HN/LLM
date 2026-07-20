# Changelog

All notable changes to LLM, newest first. Each version's installer and its SHA-256 fingerprint are on
the [Releases](../../releases) page.

## v0.18.0 — 2026-07-20

A dedicated Code tab that turns the app into a private coding workspace, syntax highlighting
everywhere, and a fix that stops large models being reclaimed in the background.

### Added

- **A Code tab.** A second top-level tab, next to Chat, with its own session list and an unrestricted,
  "finish the whole thing" coding style that keeps writing across replies until the answer is complete.
- **Projects.** Group code sessions under projects and link each project to a folder on your phone.
- **Project folder browser.** Browse a project's linked folder and load a file into your message; the
  model can read and write the project's files itself through its file tools.
- **Files.** The code the model produces is collected as named files — copy, save out, or keep as a
  snippet.
- **Snippets.** Save reusable code and drop it into any session with one tap.
- **Code quick-starts.** Ready-made starting points for building small tools you can use on the phone
  (a self-contained web page, a terminal script), for security work, and for fixing/understanding code.
- **Syntax highlighting** for code blocks in both chat and code — keywords, strings, numbers, function
  calls and shell commands each coloured.
- **Your name.** Tell the app your name and the model addresses you by it, fills `{{user}}` in
  characters, and labels your own messages.

### Changed

- **Fullscreen with real tabs.** The app runs edge to edge with the status bar hidden and a fixed
  Chat | Code bar at the very top; open the menu with a swipe from the middle of the screen.
- **Three behaviour presets** (Unrestricted, Restricted, Natural) with Unrestricted as the default; the
  two role-play presets were dropped, since a character card already carries its own role.

### Fixed

- **Large models are no longer killed in the background.** With a model loaded, the app holds itself in
  the foreground the way a terminal session does, so the phone's memory manager stops reclaiming it
  when you switch away — without keeping the CPU awake while idle.
- Character cards no longer print their own name twice in the opening greeting.

## v0.17.1 — 2026-07-19

A maintenance release: faster large models, several crashes fixed, and instructions that now reach
the model instead of being quietly relocated.

### Changed

- **Large models are faster.** The hand-tuned ARM routines that speed up quantised models were only
  enabled below a fixed 4 GB model size, so the largest models never got them. The decision is now
  based on how much memory the phone actually has free.
- **Reply length and reply language now reach the model.** Both are placed at the end of the
  conversation, immediately before the answer, where instructions are followed most reliably. Several
  model families — Gemma and Mistral among them — moved them back to the very front, behind the whole
  chat history. They now stay in place.
- **The Unrestricted preset is much shorter** and phrased as what to do rather than a list of
  prohibitions, which small local models tend to follow more literally in the wrong direction.
- **Behaviour presets can be chosen when a chat starts**, alongside the reply length. The separate
  Prompt button was removed from the menu; the full editor remains in Settings → Input freedom.
- **Adventures keep the behaviour preset** you selected instead of replacing it, and the reply-language
  setting now applies in adventures as well.

### Fixed

- The app could close while importing a large model file.
- Deleting a chat while a reply was still being written could close the app.
- Long replies could suddenly change typeface and size mid-answer, snapping back at the end.
- A short, quick swipe often failed to open the menu.
- The README's download-verification section quoted an older release's fingerprint and filename, so
  checking a genuine download reported a mismatch.

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
