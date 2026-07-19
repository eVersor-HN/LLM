# LLM v0.17.1

A private, on-device AI chat for Android. You bring the model file; everything runs on your phone.

A maintenance release: large models run faster, several crashes are gone, and instructions you give
the app now actually reach the model.

## Highlights

**Large models are faster.** The app uses a set of hand-tuned ARM routines that make quantised models
noticeably quicker, but it only switched them on for models under 4 GB — so the largest models, the
ones that need the speed most, always ran on the slow path. It now decides from the memory your phone
actually has free, which means a 6 GB model on a roomy device gets the fast routines too.

**Your instructions reach the model.** Reply length and reply language are placed at the end of the
conversation, right before the model answers, because an instruction there is followed far more
reliably. For several popular model families — Gemma and Mistral among them — the model's own format
quietly moved those instructions back to the very beginning, behind the entire chat history, where
they had little effect. They now stay where they belong.

**A shorter, calmer Unrestricted preset.** The old one was a long list of "never do this" rules, which
on small local models tends to produce exactly the behaviour it forbids. It is now brief and says what
to do instead: open with the answer, stop when the answer is finished.

**Choose the character of a chat when it starts.** The dialogue that asks how long replies should be
now offers the behaviour presets as well, so a chat can be set up before its first answer rather than
after. The separate Prompt button in the menu has been removed; the full editor lives in
Settings → Input freedom.

**Adventures keep your preset.** Starting an adventure used to replace your chosen behaviour preset
with the game master's instructions. Both now apply. The reply-language setting works in adventures
too — previously it was ignored there.

## Fixed

- The app could close while importing a large model file. Long copies are now protected from Android
  shutting the app down in the background.
- Deleting a chat while a reply was still being written could close the app. The reply is now stopped
  when its chat is deleted, and a reply that arrives too late is discarded instead of crashing.
- During long replies the text could suddenly switch to a different typeface and size, snapping back
  once the reply finished. A single indented line was enough to trigger it.
- Swiping to open the menu often did nothing if the swipe was short and quick. A short swipe now works.
- The download verification instructions in the README quoted the fingerprint and filename of an older
  release, so following them reported a mismatch on a perfectly genuine download.

## Notes

Models are files you supply yourself; nothing is downloaded for you and nothing leaves your device.
Existing chats, characters and settings are kept — this installs straight on top of v0.17.0.
