# Security

## Reporting

Report a suspected vulnerability privately, not as a public issue.

Open a **GitHub security advisory** on this repository (Security → Report a vulnerability). Include
the app version, the device and Android version, and the steps that reproduce it. Expect an
acknowledgement; a fix ships in a normal release.

Please do not post working exploit detail publicly before a fixed release is available.

## Supported version

The **latest release** is the supported one. Fixes are delivered by installing it; older versions
receive nothing.

## Authenticity

Every official binary is published on the [Releases](../../releases) page of this repository, with
its SHA-256 in the release body. The filename and the hash must both match. A file obtained from
anywhere else is not an official binary, whatever it is called.

All official releases are signed with the same key, so an update installs over the previous version.
An installer that Android refuses to install over your existing copy did not come from here.

## Trust boundaries

Stated plainly, because closed source does not justify hiding them.

**Local by default.** The app makes no network connection at all unless one of the two optional
online features is switched on. There is no account, no telemetry, no analytics and no crash
reporting.

**The two features that use a network**, both off by default:

- **Web search, open webpage, crawl.** Sends the query text or the URL to the provider you
  configured. Chat history and system prompt are not sent. Every request is shown for approval
  before it runs. Requests to private, loopback, link-local and carrier-grade-NAT addresses are
  refused, and refused again after each redirect. A hostname that resolves to a public address at
  validation time and to a private one at connection time (DNS rebinding) is not defeated by this
  check; closing that would require dialling the validated IP directly, which breaks TLS for every
  legitimate site.
- **Local API server.** Off by default. Loopback-only unless you enable LAN mode, and always
  requires the bearer token the app generates. LAN traffic is plain HTTP — treat it as you would any
  local development server, and do not enable it on a network you do not trust.

**Data at rest.** Chats, characters, imported files and settings are stored in local app storage,
encrypted at rest. Backups you export can be password-protected. Model files you import are stored
unencrypted, as they must be to be read at speed.

**The model is not a trust boundary.** A model file is executable-grade input: it decides what the
app writes. Import model files and character cards only from sources you trust. Text the model has
been given — a fetched page, a character card, a document you attached — is never treated as an
instruction to run a tool.

**What the app cannot protect against.** A rooted or compromised device, an Android build that
grants other apps access to app-private storage, or physical access to an unlocked phone. The
optional app lock (PIN or biometric) and private-screen mode raise the bar; they do not replace
device encryption and a screen lock.
