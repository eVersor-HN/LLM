# LLM v0.18.0

A private, on-device AI chat for Android. You bring the model file; everything runs on your phone.

The big one: a dedicated **Code** tab that turns the app into a private coding workspace, with syntax
highlighting, projects, and a model that keeps writing until the job is done.

## Highlights

**A new Code tab.** Tap **Code** at the top and you get a workspace built for programming instead of a
chat with a coding prompt bolted on. Sessions live in their own list, the model answers in an
unrestricted, get-it-done style, and it keeps going across replies until the whole thing is written —
no more code that stops halfway.

**Your code, organised into projects.** Group sessions under projects, and link each project to a
folder on your phone. Open a project's folder right in the menu, load a file into your message with a
tap, and let the model read and write the project's files itself.

**Files and snippets, collected for you.** Every file the model produces is gathered under **Files** —
copy it, save it out, or keep it as a reusable snippet. Snippets drop back into any session with one
tap.

**Syntax highlighting.** Code blocks are now coloured the way a modern editor colours them — keywords,
strings, numbers, function calls and shell commands each in their own colour, in both chat and code.

**A quick-start menu for code.** Ready-made starting points for building a small tool you can actually
use on your phone (a self-contained web page, or a script for a terminal), for security work, and for
fixing or understanding code — each one primed so a small local model gets it right.

**Fullscreen, with real tabs.** The app now runs edge to edge with the status bar hidden, and a fixed
**Chat | Code** bar sits at the very top. Open the menu with a swipe from the middle of the screen.

**Name yourself.** Tell the app your name and the model can address you by it; it also fills in
characters written with a `{{user}}` placeholder and labels your own messages.

## Fixed

- **Large models no longer get killed in the background.** When a model is loaded, the app now holds
  itself in the foreground the way a terminal session does, so an aggressive phone memory manager
  stops reclaiming it while you switch away — without keeping the CPU awake when nothing is running.
- Character cards no longer greet you with their own name printed twice.

## Notes

Models are files you supply yourself; nothing is downloaded for you and nothing leaves your device.
The Code tab's web tools (open a page, crawl a site) work as soon as you enable them; web *search*
still needs your own SearXNG instance or a Brave key, as before. Existing chats, characters and
settings are kept — this installs straight on top of v0.17.x.

---

**Verify your download**

```
SHA-256:  e9739f316bfbc75e8239a202ede60f633600e3905a8883e6541662c5b93ac524
```

```powershell
Get-FileHash .\LLM-v0.18.0-public-arm64.apk -Algorithm SHA256
```

The hash you get must match the value above exactly. If it does not, do not install the file.

---

> 💸 It writes code that runs on your phone. It does not, yet, write code that pays rent.
> **PayPal:** paypal.me/FAMarco
> **Bitcoin:** `bc1qv92c3eyeqvhgfnez7spfd7v2aytkhpshsl65yv`
