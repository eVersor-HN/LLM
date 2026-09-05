# Changelog

## 0.41.0 — 2026-09-05

- **Models published in several files now work.** The strongest models are often too large to be
  distributed as one file, so the people who quantize them cut them into two or three parts — and
  until now the app refused all of them, which quietly meant the best versions of GLM-4.5, Llama 4,
  dots.llm1 and MiniMax were out of reach and only their crudest single-file variants were not. In
  the file picker, press and hold the first part until it is selected, tap the rest, and confirm:
  they are imported together as one model. Choose "Import a copy" for these — a linked file is handed
  to the engine without a location, so it cannot find its other parts. A single part on its own is
  still refused, and now says what to do instead.
- **MiniMax M2 can hold a conversation.** It loaded and ran perfectly well before but could not chat,
  because the app did not recognise its turn format and said so rather than guessing. It does now.

## 0.40.0 — 2026-09-05

- **Fifty cards to start from, in six groups.** Urban survival, wilderness, tech, repair and build,
  everyday life, and people. They are practical: a power cut, water when the tap stops, a blocked
  drain, a bicycle, a wound, a letter from an office, a network that keeps dropping. The last group
  is people rather than tasks — a friend, a coach, someone who only listens, someone who argues the
  other side on purpose. None of them is written to agree with you automatically, and several exist
  specifically to disagree. Where it matters a card says where it stops: the foraging card will never
  confirm that a plant is safe to eat, the first-aid and symptom cards name the point where you call
  an ambulance instead of reading on, and the electrical card is clear about which work belongs to an
  electrician.
- **You decide what a reply is worth, and see what it costs.** Four levels above the message box —
  Fast, Normal, Thorough, Maximum — each showing the longest it can take on the model you have
  loaded. Fast answers straight away, with no reasoning step and no web lookup. Maximum gives the
  model room to work a problem through and check several sources. The limit on thinking is enforced
  rather than requested: when the budget is spent the app ends the reasoning and asks for the answer.
- **Every model shows the speed it actually reached on your phone.** Not a guess from the file size —
  the number it managed the last time it wrote something. Change the settings it ran under and the
  row says the reading no longer applies, instead of quietly standing for something else.
- **The list of families that run bigger than your memory was seven short.** Ling and Ring, GLM-4.5
  and its Air builds, OLMoE, Llama 4, Hunyuan MoE, dots.llm1 and MiniMax M2 all work and none of them
  was named — in the app or here. A 45 GB model has now been run on a phone with 23 GB of memory.
- **RPG mode has been removed, and the chats that belonged to it are deleted when the app first
  starts.** Ordinary chats, cards and models are untouched.

## 0.39.0 — 2026-09-01

- **The app speaks German.** Not a machine pass: every line was written for this app's voice, and a
  checker compares the German against the English for missing entries, mismatched placeholders and
  lost spacing before anything ships. Choose it under “App language” in the system settings for LLM.
  The Help page and a few menus are still English and fall back line by line, so nothing is ever
  blank — those follow next.
- **The interface can be translated at all now.** It could not before: every word the app said was
  written into the code. There are now 613 separate texts, and adding a language is a file rather
  than a rewrite of the app.

## 0.38.0 — 2026-09-01

- **Settings open as four choices instead of a hundred controls.** The page had grown to 105
  switches, number fields and menus across thirteen cards — enough that its own author could not
  read it. It now opens on one card: how much of the phone to spend, how you want replies written,
  what the model may talk about, and whether it may look things up. Each is a tap, each says what it
  costs you, and each one sets the dozens of values underneath it. Nothing was removed: "Show every
  setting" brings the old page back exactly as it was, and anything you had tuned by hand is kept
  and shown as "Custom" rather than quietly replaced.
- **The app stops asking to search the web for things that have not changed since antiquity.**
  "Name three Roman emperors" produced a request to look it up. The rule it was following asked
  whether an answer was "current, specific or verifiable", and almost everything is verifiable. It
  now asks the only question that matters: does the answer change over time? News, prices, versions,
  who currently holds an office — yes. History, science, definitions, how something works — no,
  answered from what the model knows. A permission prompt that appears when nothing needs permission
  is how people learn to tap Allow without reading it.
- **Adventure turns are shorter to write.** The game master had to repeat the entire character sheet
  every turn — around twenty-five lines, roughly half of everything it wrote — although the app hands
  it that same sheet at the start of every turn anyway. It now writes only what actually changed. The
  sheet on screen is identical; there is simply much less for the model to type before the story
  continues.
- **A stray dash no longer sits under every adventure turn.** Models write a rule between the story
  and the part the app reads; with that part lifted out, the rule was left behind.
- **More large models can stream their experts.** Eight more Mixture-of-Experts architectures are
  recognised, among them GLM-4.5/4.6, Ling 2.0/3.0, Llama 4, MiniMax-M2, dots.llm1, Hunyuan and
  OLMoE. Previously a model like these would load, silently fall back to holding everything in
  memory, and crawl; now the ones that are too large for RAM read their experts from storage the way
  the Qwen and Gemma MoEs already did.

## 0.37.0 — 2026-08-23

- **The app now tells you which model to get.** On first start it names the model families it can
  run straight from storage — the ones that let a model far larger than your phone's memory work at
  all — and says plainly what happens to everything else. Choosing well is the single biggest
  difference between this app being fast and being unusable, and until now nothing said so.
- **The Chat and RPG tabs no longer carry a giant letter behind them.** The empty screen is empty.
- **Saving settings saves all of them.** Changes to the tool settings or the local server made on
  the settings page were discarded by the page's own Save button. They are written now.
- **A chat with tools enabled is noticeably quicker to answer.** Work that was being repeated for
  every single word of every reply is now done only when it is actually needed.
- **Replies land in the chat they belong to.** Switching to another conversation while an answer was
  being written could grow that answer in the wrong transcript.
- **Attaching a file mid-reply no longer breaks the reply.** Attaching or importing while the model
  was writing could leave Stop doing nothing and let a second turn start on top of the first.
- **Changing a model's settings no longer locks it out.** Adjusting context size or threads on a
  large loaded model could make the app refuse to reload it, on the grounds that memory the model
  itself was holding was unavailable.
- **A short greeting no longer triggers a web lookup.** The guard against that was measuring text
  the app had added itself, so it stopped working in any chat set to short replies.
- **Chinese, Japanese and Korean chats keep working with the web tools.** The space set aside for a
  search result was calculated at the wrong rate for those scripts and could overflow the
  conversation.
- **Large text attachments no longer crash the app.** A big enough extracted document could not be
  read back, and re-opening that chat closed the app again. The document itself is untouched.
- **A failed restore no longer deletes what it restored.** If the last step failed, the files were
  removed while their entries stayed.
- **Backups estimate their size without reading your entire history.**
- **The story mode stopped rolling dice at breakfast.** Ordinary sentences — eating breakfast,
  walking along a rampart, handing over a gift — were being treated as risky attempts and resolved
  with a die. Dialogue that began "Do you…" could vanish from the story, and freeze the text while
  it was being written. A knocked-out character reads as down rather than lightly hurt. And the die
  is no longer thrown for a turn that was never sent.
- **Per-chat system prompt and format are reachable again**, in the drawer under "This chat" — the
  settings page had been pointing at a menu that no longer existed.
- **Honest labels.** The performance card says "planned" until something is actually loaded and then
  reports what the engine did; the NPU card no longer prints a placeholder instead of a size;
  "Reset model" is called "Reset settings" and asks first; Back from Help returns where you came
  from; the first-run tip names a gesture that works.
- **Heat and memory no longer undo each other.** Cooling down could hand a backgrounded app its full
  memory appetite back, which is how a background app gets closed.
- **Crawling respects "Disallow: /"** — the one robots.txt rule that was being ignored.
- **A redirect no longer carries your search API key to another site.**
- **Research with several queries works again**, instead of the searches interfering with each other
  and timing out.

## 0.36.0 — 2026-08-15

- **A chat with web search on is dramatically faster.** Before answering in such a chat the app asks
  the model a short question of its own — does this need looking up? — and asking it was throwing the
  conversation away, so every answer was preceded by re-reading the whole chat from the beginning.
  On a long conversation that was around forty-five seconds, to ask one yes-or-no question. The work
  redone before each answer fell by roughly seven eighths on the test conversation.
- **Model cards describe the file in front of you.** A vision model's note claimed the app was
  text-only, which stopped being true in v0.29.0. An eighteen-megabyte file called "llama" was
  presented like any other model with the description of the family whose name it borrowed; a file
  far too small to be what its name says is now called what it is. A model that is currently running
  no longer warns that it needs more memory than you have free.
- **The web-search switch says what it does.** While it is on, every message in that chat is looked
  up before it is answered — that is deliberate, and now it is stated, along with the fact that it
  stays on until you turn it off.
- **Starting an adventure shows progress.** The longest wait in the app offered one unchanging line
  on an empty screen. Still no numbers and no machinery, but the line moves through the wait and a
  thin rule fills as the work is done.
- **A vision model and its add-on file are no longer identical rows.** The add-on is drawn as what it
  is: indented under its model, and dimmed.
- **Photos in a chat no longer stutter the list.** They were prepared at the moment they scrolled
  into view, which held the scroll up, and were not kept afterwards — so scrolling back past the same
  photo paid the cost again. Both fixed.
- **Chats in Chinese, Japanese and Korean stop breaking early.** The estimate of how much context a
  conversation uses was written for European text and undercounted these scripts about threefold, so
  such a chat hit a hard limit and produced no answer at a third of the usable length.
- **The RAM button also hands back the browser engine** that a single web search leaves behind.
- **A gap in the private-network protection is closed** — the family of internal addresses a modern
  router actually hands out was not being checked, nor the range mobile carriers use.
- **Backup import is honest**: it does not reconcile anything, and importing the same backup twice
  gives you a second copy of everything.

## 0.35.0 — 2026-08-11

- **Models larger than your free memory now run.** A model file bigger than the memory the phone has
  spare used to be refused outright. Such a model does not need to be held in memory all at once — it
  is read from storage as it is used — so it now loads, and its card says plainly what that costs:
  "slow · reads from storage", and expect many seconds per word. A 15.6 GB model that was turned away
  on a phone with 16 GB free now opens. It is honest about being slow rather than pretending
  otherwise.
- **A RAM button in the top bar.** It unloads whatever model is resident and then asks Android to take
  memory back from other apps, and it tells you how much it actually got rather than how much it
  hoped for. Background apps may be closed to pay for it — nothing is deleted, they simply start
  fresh next time — so it always asks first.
- **And that button now actually frees memory.** Its first version was too careful with the phone to
  ever apply real pressure: it backed off within a third of a second, and measured against itself it
  gained nothing. It now keeps asking for as long as the phone can answer, and stops at the point
  where there is genuinely nothing left rather than at the first sign of effort. On a 24 GB phone with
  fifteen apps in the background it takes back around half a gigabyte where it previously took back
  none — plus whatever the unloaded model was holding, which on a 12B model is another 9 GB.

## 0.34.2 — 2026-08-10

- **Opening the model list does less work.** The processor label removed in 0.34.0 left its machinery
  behind: every time the library refreshed, the app planned a load for each model and looked up a
  saved benchmark result to decide between "CPU" and "GPU" — for an answer nothing displayed any
  more. Nothing changes on screen; there is simply less happening behind it.
- **Thermal throttling verified on the device.** No behaviour change: under severe heat a long reply
  still stops at its length limit rather than continuing itself, and that is now confirmed rather
  than assumed.

## 0.34.1 — 2026-08-10

- **The model list folds up.** Each model shows its name and only what decides whether you would open
  it: whether it is running, whether it can do something another cannot, whether it will fit, how big
  it is. Tap it and everything appears — the rest of the labels, what it is good at, and a button to
  actually use it. Five models with all their detail on screen at once was a wall, and a wall is not
  read.
- **Tapping a model no longer loads it.** It used to, which meant brushing a 23 GB model in a list
  started reading it from storage. Loading is now something you ask for.
- **The model's own notes-to-self stopped appearing in its replies.** A model that thinks before it
  answers can stop and restart that thinking; only the first block was being removed, so the second
  reached the chat — reasoning, self-corrections and a stray marker in the middle of the answer.
- **A greeting no longer triggers a web search.** With web search on, "hi" was producing a request to
  research "Who am I?" — harmless, because it asks first, but a permission prompt on every greeting
  teaches you to wave it through.

## 0.34.0 — 2026-08-10

### Every model says what it is

- **Model cards carry labels now.** A GGUF file tells you almost nothing about itself, and the card in
  the library is the only place the app can. Each one shows what the model *is* — its weight format,
  its size, whether it can see pictures, whether it is a Mixture-of-Experts model that runs from
  storage although it is larger than your memory, whether it is linked rather than copied — and, for
  the one model that is loaded, what it is *doing*: the processor it is actually running on.
- **Four weights, and the weight carries the meaning.** A filled label is the running model. An
  outlined accent label is an ability another model may not have. A quiet outlined label is a plain
  property. A warning label means it will not load as things stand, and says what is needed. Colour is
  never the only signal — every label says its meaning in words, because the app has a colour-vision
  setting.
- **The guessed processor label is gone.** Every card used to carry "CPU" or "GPU" in the shape of a
  fact, while guessing at a plan that had not been made yet. Only the loaded model is labelled now,
  and that label comes from the engine.
- **A loaded model no longer mislabels itself.** Once loaded, a 6.9 GB model was announcing "runs from
  storage" — the library was measuring it against the free memory that the model itself was occupying.

### Fixed

- **The frozen prompt tail survives a backup.** Restored adventures kept their invisible turns but
  lost the record of what the model had actually been told on each one.

## 0.33.2 — 2026-08-10

### A model card now describes the model that is running

- **The acceleration badge stopped guessing.** It decided "⚡ CPU + KleidiAI · Q4_0 fast path" from
  the quantisation and a 4 GiB size limit — a rule the engine removed long ago as wrong in both
  directions. Those fast ARM kernels come from a weight conversion the engine performs only when
  there is memory for it (twice the model plus 2 GiB), and every k-quant benefits, not only Q4_0. A
  small Q4_0 on a busy phone was promised a fast path it never got; a 6.9 GB Q4_K_M running on
  exactly those kernels was labelled "large". The engine now reports what it did and the badge
  repeats it.
- **A model on the NPU is no longer badged "CPU".**
- **"The NPU is used automatically" was not true** and no longer claims to be. Automatic always
  resolves to a CPU profile; the NPU has to be chosen. Both places that said otherwise now say what
  to pick and why you might not want to — it processes long prompts far faster and writes more
  slowly.
- **A Mixture-of-Experts model is no longer refused against a number the engine never uses.** The
  estimate treated the 6 GB cache ceiling as a requirement; the engine sizes that cache to the phone
  it finds. On a device with modest free memory that refused models which would have run.
- **The memory figure in the model list is the one the load will use.** It was computed for a
  different profile, with twice the context, so it quoted hundreds of megabytes too much.
- **The performance line and the diagnostics report say what runs, not what was requested** — token
  generation is capped at four threads, the batch is clamped to the context, and memory-mapping is
  switched off whenever the weight conversion happens.
- **The memory watchdog can now be seen to have run.** Release builds strip every log call this app
  makes, so the one mechanism watching for a rare, hard-to-reproduce condition had no way to show it
  had ever measured anything. Its readings and how often it had to act now appear in the diagnostics
  report.

### Fixed

- **A linked model was pinned to the CPU forever.** The benchmark that chooses between CPU and GPU
  was handed the model's location instead of its contents, failed both runs, and cached the failure
  as a decision.
- **Downloads could not resume**, despite saying so: each attempt started a new one, and the
  abandoned part became invisible to the app and to you. An interrupted download of the same file is
  picked up now, and a dropped connection continues from where it stopped instead of discarding
  everything.
- **A download can no longer be silently corrupted** by a server that answers a resume request with
  the whole file.
- **Expert streaming is no longer announced for a model that will not stream** — it was decided
  against memory the model being replaced still occupied, and the "force streaming" switch was
  invisible to the check that could refuse the model it was turned on for.
- **The drawer is readable at the largest text sizes.** The header buttons were being broken
  mid-word ("GGU / F") and the three counters ran into one another.
- **An adventure's opening turn is recorded the way it was sent.**

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
