# Changelog

All notable changes to LLM, newest first. Each version's installer and its SHA-256 fingerprint are on
the [Releases](../../releases) page.

## v0.14.4 — 2026-07-18

### Changed

- Each built-in character now shows a one-line description of what it actually does, instead of six
  identical "Tap to start a new chat" subtitles.

### Fixed

- Editing a message now happens right where the message is, in the app's own styling. It previously
  opened a plain system dialog in the middle of the screen, nowhere near the text you were editing.

## v0.14.3 — 2026-07-18

### Added

- Six built-in characters, ready the moment you open the app — an engineer, an analyst, a teacher, a
  writer, a philosopher, and one deeply sarcastic machine. Tap any of them to start a chat where they
  greet you and stay in role.
- The Cards list is now split into "Your cards" and "Presets", each collapsible with a count, so
  imported cards are never buried under the built-ins. Both sections stay open while you search.

### Fixed

- Returning to the app no longer flashes "Load a model to begin" and an import button over a chat that
  is already there. The welcome screen now waits until your chats have actually been read.

### Notes

- Built-in cards are seeded once. Delete one and it stays deleted; edit one and an update will not
  overwrite your version.

## v0.14.2 — 2026-07-18

### Added

- Support for on-device NPU acceleration on recent Snapdragon phones, with a large speed-up when a
  reply has a lot of prompt to read first — long character cards, roleplay, or a long history.
  The app picks the right processor per model on its own.
- A per-model chip in the model list showing which processor that model will use.
- Markdown tables now render as a real grid.
- A jump-to-latest control that appears only when you have scrolled up.
- A collapsible Help & FAQ section in Settings.
- A redesigned launcher icon.

### Changed

- Releases are now signed with a stable key, so from this version on updates install on top of each
  other without uninstalling first.
- The release build is shrunk and obfuscated, and the native library ships stripped.
- The local API access token is encrypted at rest.

### Fixed

- Reply length (Short / Medium / Long) now always takes effect, including on a brand-new chat, and a
  new chat keeps the length you were using.
- Continuing a long reply no longer injects a visible restart artifact into the text.
- Restored a reliable menu button for the navigation drawer, which the system back gesture could
  swallow when opened by edge-swipe.
- Raised low-contrast text and small touch targets to meet accessibility minimums.
- Switching to an equal-or-larger model is no longer falsely blocked by the memory check.

## v0.14.0 — 2026-07-15

### Added

- Optional app lock with PIN, password or fingerprint, with a timeout and delays after failed attempts.
- Encryption for locally stored chats and library metadata.
- Optional password-encrypted portable backups.
- Automatic context trimming in model chat: the oldest turns are dropped to fit the loaded model's
  context, and you are told how many were omitted.
- A device list showing the accelerators the app actually found on your phone, rather than guessing.

### Changed

- Multi-turn chats now reuse the work already done on earlier turns instead of re-reading the whole
  conversation each time, so replies start sooner.
- System and cloud backup of app data is disabled, so your chats are never copied off the device by
  Android.
- Unsandboxed shell execution is a separate permission and is off by default.
- The local network API gained per-client rate and connection limits and shuts down when Wi-Fi is lost.
