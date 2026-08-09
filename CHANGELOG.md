# Changelog

## 0.33.1 — 2026-08-09

- **A model card no longer claims a model streams its experts when it does not.** A Mixture-of-Experts
  model that comfortably fits in memory is loaded resident, because that is faster — streaming is what
  happens to one that does not fit. The library asked only whether the ARCHITECTURE could stream, so a
  7 GB Gemma 4 was described as "streams experts · needs ~13.6 GB free" while the engine loaded it
  resident and used about 9 GB. The card described a different model from the one running, and the
  safe-load check was sized against the wrong number with it.

  Fixed where such bugs have to be fixed: the condition now lives in one place beside the loader's own
  decision (`llmc_moe_will_stream`) and both sides call it, rather than two places agreeing until they
  drift. This is the third bug of exactly this shape — the model-name test versus the recipe registry,
  the projector paired by guesswork, and now "could stream" versus "will stream".

## 0.33.0 — 2026-08-09

### Models

- **Download a model straight from a link.** Drawer → GGUF → *From a link*, paste the address of the
  `.gguf` file, and it lands directly in the app. Until now a model arrived in two moves — fetch it
  in a browser, then import it — and the import copies, so a 23 GB model needed 46 GB of free space
  and a long wait after an already long wait. A download that stops keeps what it has; paste the same
  link again and it continues from there.
- **Or keep the file where it is and never copy it at all.** Picking a GGUF now asks: *Import a copy*
  puts it in the app's own storage as before, *Use where it is* only remembers permission to read it.
  A 23 GB model then costs 23 GB instead of 46 and appears in the library at once. The file has to
  stay put — moved, renamed or deleted, the model says exactly that — and deleting such a model from
  the library never touches your file.
- **A model's own file name is remembered.** Projector pairing and the expert-cache autotuner are
  decided on it, and a linked model has no path to read it from.

### Dictation

- **Dictation now runs on the device where the device can do it.** Android 12 and newer offer a
  speech recogniser that transcribes without a network; the app asks for that one first. The entry in
  the "+" menu says which one you got — *on this device*, or *uses a speech service* — because in an
  app that otherwise sends nothing anywhere, that is not a detail to leave unsaid.

### While a reply is being written

- **The percentage meant two different things and ran backwards.** It showed how much of the prompt
  had been read, and then, from the first token, how much of the length limit the reply had used —
  so it climbed to 99 % and dropped to 2 % in front of you, twice per turn with auto-continue. It now
  measures one thing, the prompt, and only while that is happening: *"reading the conversation · 42 %"*.
- **A token counter takes its place while the model writes.** It only ever goes up, which is the
  honest version of "something is happening" — the length limit is a cap, not a target. It matters
  most when nothing is rendering: a reasoning model can produce tokens for a minute behind a hidden
  thinking block.

### Adventures

- **An adventure no longer re-reads its whole story every round.** The turns you play were fed to the
  model and then thrown away, so the next round's history no longer contained them and the cached
  context diverged at your previous move — every round re-read everything after it, including the
  last game-master reply. Those turns are kept now (still invisible in the story), and the per-round
  material is frozen onto the turn it belongs to instead of being recomputed.

### Memory

- **The app now notices memory pressure while you are looking at it.** Android stopped delivering the
  "running low" signals to apps in its current versions, so the expert cache only ever shrank once the
  app had been sent to the background — never during the long reply that caused the pressure. It is
  measured directly now, against the device's own kill threshold, and said out loud when it happens.

### Fixes

- **A backup restore no longer wipes settings it never carried.** The SearXNG address and the two
  network switches were reset on restore although they are deliberately not exported, so restoring
  your own backup silently removed a self-hosted search endpoint. They are left alone now — and a
  backup still cannot switch network access on.
- **Long menus open next to the button they belong to.** A seven-language list at a large text size
  was flipped a screen away, over unrelated settings.
- **Two dialogs stopped cutting their own explanation off** at the right edge.
- **The composer's buttons grow with the text size.** At the largest sizes they sat small and low
  beside a field twice their height.
- **A very small model is no longer mistaken for a vision add-on.** The rule that recognises a
  projector by shape had no lower bound, so any tiny GGUF without a chat template was captioned
  "loads with its model" — a claim about a file that does not exist.

### Under the hood

- Dictation, clipboard and lifecycle now use the current APIs; the build has no deprecation warnings
  left.
- The prompt-tail rule that decides whether the cached context can be reused at all is a plain,
  tested function now, with the measured failure it came from kept as a test.
- The app declares itself as a game to the system, which is how phone vendors gate their CPU and
  thermal boost paths — measured elsewhere as the difference between a middling clock and the
  hardware maximum.

## 0.32.0 — 2026-08-03

### Vision models find their projector

- **A vision model now pairs with its projector even when the file names are all you have.** Pairing
  compared only the names stored *inside* the two GGUFs — and a converter is free to leave that as
  the base model's, or blank. The Qwen3-VL projector ships as a bare `mmproj-F16.gguf`, which scored
  zero against the very model it was exported for. The file names, which publishers do keep in step,
  are now compared too.
- **A projector is no longer guessed onto the wrong model.** With one projector in the library the
  app used to attach it to whatever was loading, on the reasoning that there was nothing else it
  could belong to. With gemma + its projector + a second vision model, that handed the *gemma*
  projector to the second model — the one projector present that demonstrably belonged elsewhere.
- **The parameter count now settles it.** Everything a publisher ships carries their handle and the
  family in front: `Huihui-Qwen3-30B-A3B-…` and `mmproj-Huihui-Qwen3-VL-8B-…` share twenty-two
  characters without being related at all, which was enough to label a text-only 30B model "Vision".
  A size that both names state and that disagrees — `30b` against `8b` — now rules the pair out, and
  no amount of shared prefix outvotes it.
- **A vision model whose projector you never imported says so.** Its card was identical to a
  text-only model's, so the missing half was invisible: the file is there, it chats, and the only
  symptom is a *Vision* label that never appears. The card now says which file to look for.
- **Deleting re-derives the labels.** Removing a projector left its model still labelled *Vision* —
  a claim with nothing behind it — until the next import or restart.

### Models bigger than your memory

- **Qwen3-VL MoE models stream their experts again.** The streaming engine had no recipe for
  `qwen3vlmoe`, so a 30 GB vision MoE quietly fell back to ordinary memory-mapped loading and
  thrashed: 83 seconds to read a single image. It now streams like every other Qwen3 MoE.
- **The app no longer promises streaming it cannot deliver.** Two places decided whether a model
  streams, and they disagreed: one asked whether the architecture name contains "moe", the other
  asked the engine's recipe list. A model that passed the first and failed the second was admitted
  against a memory estimate of the *streaming* working set and then loaded whole. Both now ask the
  engine.
- **Help opens with what this app is for.** How a 30 GB model runs on a phone with 8 GB free, which
  model families can do it, and how to recognise one before you download it — first section, before
  everything else.
- **The library says what a streamed model costs.** "streams experts · needs ~8.1 GB free" is a
  promise and an apparent contradiction; underneath it now says, in plain words, that file size is
  not the limit and that you should expect seconds per word.

### Fixed

- **A model could lock itself out of its own chat.** The memory check credited back the model being
  replaced — but only a *different* one. Re-selecting the model that was already loaded credited
  nothing, so a 23 GB MoE was measured against memory that this very model was occupying: "needs
  about 8.2 GiB and only 7.3 GiB is safely available", with the 7.2 GiB it was itself holding
  invisible to the sum. The bigger the model, the more certain it was to happen.
- **A refused load no longer claims nothing is loaded.** The check runs before anything is unloaded,
  so whatever was resident still was — but the app reported otherwise, and the memory readout and
  the Free button both went along with it.
- **"I can only see `<media>`."** The marker that tells the projector where an image goes is plain
  text in the prompt. A model that echoes it leaves one behind for good, and every later turn then
  sent a marker with no image — so the model correctly reported seeing a placeholder and nothing
  else. Markers are now stripped from replayed history and re-added only for images actually
  attached.
- **Roughly 200 MB written to storage after every reply.** The conversation cache was saved whenever
  a chat had more than one message, but the file's size follows the whole cache allocation rather
  than how much of it is used — one saved reply cost 182 MB to preserve a single token. The rule now
  counts what is actually cached.
- **Web search worked out of the box everywhere except in the setting that decides it.** The default
  is documented as the built-in browser, and the browser is the only path that can show a
  "confirm you are a person" page — but the settings loader handed out SearXNG to anyone who never
  opened Settings → Tools. Searches went to public servers that now answer with a rate limit, and no
  check could ever appear.

### Plainer words

- Memory warnings dropped the vocabulary of the implementation. "Safe-load check blocked this
  configuration: estimated peak 8.1 GB, safe budget 7.3 GB" said what the machinery did; it now says
  what is too big, by how much, and which of your options changes it.
- "Resident" is gone from the two places you could read it. It meant "in memory", so it now says so.

### Removed

- Five leftovers from features that were deliberately taken out and whose code stayed behind: the
  prompt-mode switch, the active-card indicator, a drawer row for two sections that no longer exist,
  the CPU/GPU badge, and the adventure re-roll that went when free-text play arrived. Eighty-nine
  lines, none of them reachable.

All notable changes to LLM, newest first. Each version's installer and its SHA-256 fingerprint are on
the [Releases](../../releases) page.

## v0.31.0 — 2026-08-02

### Web search works on a phone that was just installed

- **Search no longer needs anything set up first.** Every public SearXNG server the app used has
  stopped answering: three rate-limit anything that is not a person, two reply with a “verifying you
  are human” page, one is gone. A fresh install could therefore not search at all, and the only
  remedy on offer was to type in the address of a server you host yourself. Search now runs through
  the browser engine Android already has — no configuration, no account, no API key.
- **When a page asks whether you are a person, it asks you.** The check appears in the app, on the
  page that wants it. The app does not solve it for you; the answer is remembered for a while.
- **What it costs, plainly.** The search page loads in full, with its scripts and cookies, as it
  would in your normal browser. Third-party cookies are refused and images are not downloaded, but
  the search engine sees your query. The model still runs entirely on your device.
- **Your own SearXNG is still better** — plain data instead of a web page, no checks, nothing
  leaving hardware you own — and is now a choice rather than the price of entry.

### Fixed

- **“Web search” switched on everything except the crawler.** The toggle forced on search, page fetch
  and research but left the crawler at a global setting that is off by default, so the one tool that
  can follow a trail was silently missing.
- **A local address now says why it cannot work.** `http://127.0.0.1:8888` reaches a computer on your
  desk only while the phone is plugged into it.

## v0.30.2 — 2026-08-02

### Added

- **The model list says that a model does not have to fit in your memory.** A Mixture-of-Experts
  model reads only the part it needs for the word it is writing, straight from storage, so one
  several times larger than your free memory still runs. Until now the only trace of that was a
  “streams experts · needs ~8.1 GB free” under a 30 GB file, which reads like a typo. A short note
  above the model list explains it, expands for the detail, and can be dismissed for good.

### Fixed

- **Dialogs ignored the text size you set.** Every screen followed the accessibility text slider
  except the dialogs — where the short, important sentences live. They grow with the rest now.
- **Long labels were cut in half instead of wrapping** at large text sizes: the drawer buttons, the
  free-memory line and the donation row.
- **A lookup searched the wrong year.** The model cannot know today's date, so a question about
  something current was searched as though it were still the year it was trained in. The date is
  part of what it is told now, and “hello” no longer sends anyone to the web.
- **The vision add-on warning interrupted every model load**, including for models that have nothing
  to do with images. It is raised when a photo is actually refused, and clears itself when a pairing
  later succeeds.
- **A scanned PDF said “no readable text was found”** instead of suggesting a photo of the page,
  which a vision model can read. Its pages are pictures, and pictures were not being counted.
- **Every RTF attachment began with its own font list** — the font table, colour table and
  stylesheet a word processor writes before the first sentence were handed to the model as text.

## v0.30.1 — 2026-08-01

A correction to 0.30.0. If you use a vision model, please update.

### Fixed

- **A vision model was refused and then permanently marked as text-only.** 0.30.0 compared the
  model's embedding size with the projector's and rejected the pair when they differed — two numbers
  that were never comparable, because a projector's file describes its own vision tower. Since the
  capability is recorded after a load, the model then stayed labelled text-only for good. This
  version repairs the label on the next start; nothing needs re-importing.
- **A model says it can see before it has ever been loaded.** The “Vision” marker used to appear only
  after the first successful load, so a freshly imported model and projector looked text-only. The
  library is read directly instead, in both directions, and the marker is corrected in both
  directions too.
- The About screen credits **eVersor-HN**.

## v0.30.0 — 2026-08-01

The model looks things up, and replies stop re-reading the whole conversation.

### Added

- **Web search that actually searches.** Turn on “Web search” in the + menu and the model searches
  before it answers instead of relying on a memory that stops at its training date. Until now it
  ignored the ability entirely — asked who the economics minister is, it named the previous one, and
  nothing about the answer looked wrong.
- **“Research” does the whole lookup in one step**: several searches at once, the most promising
  results opened in parallel, split into passages, ranked against your question, and handed to the
  model as a short numbered set of sources.
- **Answers cite what they read.** Sources are numbered and the reply points at them — “…elected with
  325 votes [4]”, where [4] is the page that says so.
- **A lookup appears as a card**, not a wall of text: the tool that ran, a one-line summary and the
  sources, with the passages folded away behind an arrow. Tap a source to copy its address. A failed
  lookup is marked in red and says why.
- **A crawler that follows the trail on purpose.** Give it a starting page and something to look for
  and it visits the most relevant links first, with three breadths — a few pages, one site, or off
  across the web on mains power.
- **Help explains self-hosted search**: what SearXNG is, how to run one, and the two settings that
  decide whether it works with the app.

### Changed

- **Replies get faster the longer you talk.** Each turn no longer rebuilds the model's context from
  scratch. On a four-turn chat, 914 of 1002 tokens were reused and 88 processed instead of 1002; a
  two-turn exchange went from 23 to 12 seconds, and the saving grows with the conversation.

### Fixed

- A tool request written by the model **was thrown away** unless the reply contained nothing else, so
  a model that wrote one polite sentence first was ignored.
- A **self-hosted search server could not be reached at all**, because Android refuses plain HTTP.
- A **vision add-on was attached to models it cannot belong to**, and the failure only flashed by in
  the status line. It now refuses a pairing the files disprove and explains it.
- A **research result could be too large to answer** — a perfect set of sources arrived and the reply
  never came. It is now sized against the space actually left.
- The Adventure tab's opening screen had **no way to start an adventure**.

## v0.29.0 — 2026-07-29

Photos and documents, and replies that reach the answer.

### Added

- **Show the model a photo.** Tap “+” → Attach a photo, write your question and send. With a vision
  model loaded it describes what is in the picture, reads the text on a printed page, translates a
  sign, or explains a diagram — and the photo stays visible in the chat above your message. Any
  format your phone can open works, HEIC and WEBP included; pictures are scaled down before the model
  sees them, so a 12-megapixel photo does not turn into minutes of waiting.
- **A vision model sets itself up.** Import the language GGUF and its mmproj file and the app pairs
  them by name when the model loads — nothing to configure. A projector on its own is labelled
  “vision add-on · loads with its model” and no longer pretends to be a model you can talk to.
- **Attach a PDF, Word, Excel, PowerPoint, OpenDocument, RTF or EPUB file and the text comes out.**
  On your device, with no library and nothing sent anywhere. Tap “Insert text” and it lands in your
  message where you can read it, shorten it and ask your question around it — nothing goes to the
  model behind your back. Spreadsheets keep their rows and columns; presentations are labelled by
  slide.
- Files that genuinely cannot be read say so instead of returning noise: a scanned PDF (photograph
  the page and use a vision model instead), a PDF whose text is locked inside custom font tables, and
  the pre-2007 binary .doc/.xls/.ppt formats.

### Fixed

- **Replies that stopped after the model's thinking.** On models that separate reasoning from answer,
  generation ended silently at exactly that seam — so the reply you got was the model's private
  notes, and the answer never arrived.
- **Reasoning is folded away again** into “▸ Reasoning” instead of being glued onto the front of the
  answer.
- **The attached picture never reached the model.** It does now. The question was answered about a
  photo the model had never been shown.
- The attachment bar no longer says “nothing is inserted automatically” over a photo — a photo is
  sent with your message, which is the whole point of attaching one.

## v0.28.0 — 2026-07-29

Very large models load again, adventures are played by writing instead of picking, and the app tells
you what each model needs before you tap it.

### Added

- **Play an adventure by writing what you do.** The RPG tab no longer offers a short list of options
  to pick from. You type your action in your own words, in the same box you chat in — talk to someone,
  search a room, lie, run, climb out of a window. When what you try could fail, the game master rolls
  the die and it falls across the screen; shake the phone while it is in the air and it keeps
  tumbling until you stop.
- **Realism, per character card.** A switch on each card in the drawer. On, the character is played
  as a person with their own mood and reasons, who can hesitate, ask their own questions or need to
  be won over — instead of agreeing with everything immediately. It changes how a scene feels, not
  what is allowed, and it applies from the next message so you can turn it on mid-chat.
- **See your memory, and get some back.** The drawer shows how much of your phone's memory is free,
  live. When a model is loaded there is a "Free" button that unloads it and hands the memory back —
  and it reports what was actually freed rather than promising anything.
- **Every model says what it needs.** Each model in the list shows the free memory required to load
  it, and turns red when your phone cannot currently satisfy it. Large Mixture-of-Experts models show
  their real (much smaller) requirement instead of their file size.
- **"Skip cold experts" for large models** (Settings → Device and performance). Roughly two thirds
  fewer reads from storage and a clear speed-up on big models, at the price of slightly different
  wording and answers that are no longer word-for-word reproducible. Off by default.

### Fixed

- **Large Mixture-of-Experts models refused to load.** A model of 20 GB or more could be turned away
  with "Model too large for this device" even on a phone with plenty of memory free — the very case
  the app was built to handle. Three separate causes, all corrected; such a model loads and answers
  again.
- **Big models got slower the longer you owned them.** The app tunes itself to your phone, and it
  could mistake being closed in the background for running out of memory — then quietly give itself
  less to work with, again and again, with no way back. It now tells the two apart, and refuses to
  settle on a setting that is measurably too small.
- **The die was thrown again when it should not have been** — on reopening a story, and after
  scrolling up and back down.
- **A single oversized chat, model entry or reply could make the app unusable.** It now keeps working
  and says what happened, instead of leaving you with no way to reach the item and delete it.
- Opening the drawer no longer stutters while it reads your memory.

### Changed

- **Tablets, foldables and large screens.** Text keeps a readable width and stays centred instead of
  stretching across the whole screen, so the app looks the way it does on a phone, with margins.
- **Adventure setup**: the six setting tiles are now identical in size with centred labels.
- **Character sheet**: the sixteen attribute tiles are folded away behind one heading, with the
  values you check most still visible on it.
- Help has been brought up to date and covers memory requirements, realism and the new RPG.

### Security

- Diagnostic logging no longer contains anything that could be turned back into what you typed.

## v0.27.1 — 2026-07-28

Groundwork for making follow-up replies faster.

### Changed

- **Less wasted work on follow-up questions.** When a conversation continues exactly where it left
  off, the app no longer discards the work it had already done on that conversation. Some model
  families benefit from this more than others, and long conversations do not benefit yet — see below.

### Known

- **Follow-up replies in a long conversation still take as long as the first one.** The app currently
  re-reads the whole conversation for every reply instead of only the new part. The cause is now
  identified and this release contains the first half of the fix; the rest changes how instructions
  are placed in the prompt and is being done carefully rather than quickly, because it can affect
  reply quality.

## v0.27.0 — 2026-07-28

The app now notices when your phone is struggling and eases off, and Settings stops throwing away
work you have not saved.

### Added

- **It backs off when the phone gets hot.** When your device heats up or switches to battery saver,
  the app quietly narrows how hard it works instead of pushing on until Android throttles it. Long
  replies stop being extended automatically while that lasts, so a hot phone gets a shorter answer
  rather than a slower one and a flat battery.
- **A Stop button on the notification.** You can end a reply from the notification shade without
  opening the app, and it saves what was written so far, exactly like the Stop button in the chat.
- **Settings asks before discarding your changes.** Leaving the Settings page with unsaved edits now
  offers to save them. This covers all three places on that page that have their own Save button.
- **You can check who signed your copy.** Settings → About shows the signing fingerprint of the
  installed app. Compare it with the release notes: a different value means the build did not come
  from the developer. Useful after installing, where the file hash can no longer help you.

### Changed

- **Tapping the notification no longer restarts the app.** It used to close and reopen the app,
  which threw away the reply it was announcing.
- **The RPG drawer reads in the story's font.** The character sheet, chronicle and choices now follow
  the reading font you picked, and the Chat | RPG tabs no longer change size with the story text
  slider.
- **Clearer attribution.** The licence screen now describes the optional NPU files and the toolchain
  they were built with.

### Fixed

- **The app no longer closes itself in rare cases.** A refusal by Android to keep the app running in
  the background is now reported instead of ending the process, and unusual model or card files can
  no longer take the app down while being read.
- **Backups round-trip more safely.** A protected value that could not be read on export is no longer
  made permanently unreadable by importing it again.

## v0.26.0 — 2026-07-27

A reliability and safety release: more models load, your data is better protected, and you can keep
notes on your models.

### Added

- **Notes on your models.** Every model in the list can carry a short note — what it is good at, what
  it is not — so you stop guessing which file was which. The app fills in a first suggestion from the
  name; edit it or replace it and it becomes yours. Collapsed it stays a single quiet line so a long
  note never floods the list; tap to read the whole thing.

### Changed

- **More models just work.** Newer model families that previously would not start now load and chat
  correctly, and large models that used to quit partway through loading come up cleanly.
- **Reopening a conversation is near-instant** even for a big model.
- **Formulas display properly** — inline math in a reply now renders instead of showing raw markup.

### Fixed

- **Your local chat text is now protected on your device** — drafts, saved conversation settings and
  story journals are no longer kept in the clear.
- **Backups always restore.** A backup can no longer be produced that the app then refuses to load,
  and older backups still restore exactly as before.
- **Nothing gets lost quietly.** A conversation you configured, a draft you were typing, or a model's
  answer you interrupted are all kept where they used to occasionally vanish.
- **Malformed model cards are handled safely** instead of freezing or crashing the app, and a story
  can no longer be knocked into a state where it will not reopen.

## v0.24.1 — 2026-07-26

A small RPG quality-of-life patch on top of v0.24.0.

### Changed

- **The character sheet explains itself.** Tap any value on the RPG sheet — the eight attributes,
  every derived value (defence, attacks, initiative, the passive senses, carry capacity) and the
  saving throws — and a small popup tells you in plain language what it is and when the story uses
  it. A quiet hint on the sheet points the way.
- **Sheet rows regrouped** so each line reads as one idea: body & senses, mind & presence, the
  fight, and what you notice and can carry.

## v0.24.0 — 2026-07-26

A polish release across the whole app: smoother streaming, a calmer RPG, and Settings you can
actually find your way around.

### Changed

- **Settings reorganized.** Reply behaviour (length, language, emojis, auto-continue, auto-scroll)
  now lives in one "Chat & replies" card; the reading font is under Appearance; screenshot blocking
  under Privacy; and Accessibility is genuinely about accessibility again, including read-aloud.
  Every setting on the page now applies immediately — no more scrolling down to "Save" for half of
  them.
- **Calmer RPG.** While the story writes you see a quiet pulse instead of a progress readout, and
  chat controls (continue prompts, reply variants, edit menus) no longer appear over the fiction.
  All icons in the adventure setup are now the app's own monochrome style.
- **Reduce Motion now covers the adventure too:** choices appear instantly and the dice verdict is
  shown without the throw and slam. The dice result is also announced to screen readers.
- **Smoother, lighter streaming.** Long replies stream with noticeably less overhead, switching
  between long chats is snappier, and the app starts a little faster.

### Fixed

- Story text no longer changes its spacing the moment a turn finishes writing.
- World notes are properly removed when their adventure is deleted, and travel with backups.
- The battery-optimisation status in Settings updates right after you grant the exemption.
- Several small battery and stability fixes around tool approval and low-memory situations.

## v0.23.0 — 2026-07-25

Focused on Chat and RPG: a more immersive text-adventure mode, a lighter app, and smoother, more
stable generation.

### Added

- **World notes for RPG.** Keep the places, people and secrets of your adventure as notes; the game
  master is reminded of each one exactly when it matters, so a large world stays consistent without
  slowing the game down.

### Changed

- **The app is now Chat + RPG.** The Code tab has been removed to keep the app focused and clean; your
  existing chats are unaffected.
- **Nicer RPG reading.** Story text now reads like a book, with roomier line spacing and paragraph
  rhythm.
- **Smoother streaming.** A reply now streams without making the rest of the screen do unnecessary
  work, so scrolling and typing stay responsive while the model writes.
- **Leaner and safer.** Removed the experimental tools that let the model run shell commands and touch
  files, so the app no longer requests those permissions. Web search, the calculator and the local API
  server stay.
- Updated the in-app Help with guidance on running very large (20–30 GB) models and how much memory
  they actually need.

### Fixed

- RPG choice buttons no longer show stray tags like "[STR]".
- Better stability on phones that could kill a very large model while it was loading.
- A lighter dice animation, and an extra safety check when reading a character-card file.

## v0.22.1 — 2026-07-24

### Fixed

- **Crash on first start with a very large streaming model.** On some phones with aggressive memory
  management, loading a model much larger than RAM (and starting a new RPG) could get the app killed by
  the system during loading. The app now uses a more conservative memory budget — especially on the
  very first load — so it stays alive. Verified on a 24 GB phone with a ~24 GB model.

## v0.22.0 — 2026-07-24

Smarter memory handling for models larger than your RAM, a cleaner message bar, and fixes for how the
Chat / Code / RPG tabs behave.

### Added

- **Smarter streaming memory.** For a model that streams its experts from storage, the app now learns
  the right amount of memory to cache per device and per model, and backs off automatically when it
  detects the phone is being pushed too hard — including under memory pressure or when the phone gets
  hot — so big models stay stable instead of getting killed. You can also turn on "Force MoE expert
  streaming" (Settings → Device & performance) to stream a model even when it would fit, for a smaller
  memory footprint. A small status line shows when a model is streaming and how it's tuned.
- **Cleaner message bar.** The attach, dictate, and web-search buttons now live in one "+" menu, so the
  text field is much wider. New hand-drawn icons replace the old emoji symbols.

### Changed

- The **Adventure tab is now called RPG**.

### Fixed

- A reply is no longer visible in more than one tab at once — the live text now stays in the tab where
  you started it.
- Typing a first message on the Code tab now starts a proper code session instead of an ordinary chat.

## v0.21.0 — 2026-07-23

Run a model larger than your phone's RAM: a Mixture-of-Experts model can stream its experts from
storage as it writes. Plus Adventure mode and dictation since the last public build.

### Added

- **Models larger than RAM.** For a Mixture-of-Experts model (e.g. Qwen3-30B-A3B), the shared weights
  stay in memory while each word's experts are read from storage on demand — so a 25–30 GB model runs
  on a phone that can't hold it all. Engages automatically, and only when a model won't otherwise fit;
  smaller models load exactly as before.
- **Adventure mode.** A third tab: a text-adventure game master with a shake-to-roll d20, thrown-dice
  animation, a character sheet that fills in as you play, and a story chronicle in the drawer.
- **Dictation.** Speak your message from the composer instead of typing.

### Fixed

- Large MoE models no longer get killed by the system while loading: streaming keeps a capped memory
  budget, overlaps storage reads with compute, and the loader no longer pulls the whole file into
  memory at once.

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
