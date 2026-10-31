# ntts-translator

**Nerd -> Normal.** Translates status codes, error messages and IT jargon into plain German or English.

Default mode is **tl;dr**: paste `clientHold domain registrar` and you get back `scam go bye bye`.
Switch to **ausfuehrlich / detailed** for a full explanation of every match.

## Features

- Works fully offline, single `index.html`, no build step, no dependencies
- ~200 entries, detected anywhere inside pasted text/logs:
  - HTTP status codes: all official ones (100-511) plus unofficial ones (419 Laravel, 444/499 nginx, 520-530 Cloudflare, 529)
  - Domain status (EPP): clientHold, serverHold, *Prohibited locks, redemptionPeriod, pendingDelete, ...
  - DNS: NXDOMAIN, SERVFAIL, REFUSED, ...
  - Linux errno: ENOENT, EADDRINUSE, ECONNREFUSED, ...
  - Exit codes and signals: 126, 127, 130, 137, 139, 143, segfault, OOM
  - Browser / TLS: CORS, ERR_CERT_*, ERR_TOO_MANY_REDIRECTS
  - Git, pacman (Arch), Python / Node / Java errors
  - Discord API and Gateway codes (50013, 10062, 40060, 4004, 4014, ...)
  - Common jargon (rate limit, upstream, TTL, regression, EOL, ...)
- Language toggle: German / English
- "Nachschlagen" tab: search and filter every entry
- AI translation button for unknown text (only available when opened as a claude.ai artifact; hidden elsewhere)

## Usage

Open `index.html` in a browser. Or enable GitHub Pages for this repo (Settings -> Pages -> Deploy from branch `main`, folder `/`).

## Adding entries

All entries live in the `D` array in `index.html`:

```js
["404","http","bad","Not Found","German text","English text","tl;dr line"],
```

Format: `[key, category, severity (ok|info|warn|bad), name, de, en, tldr, optional regex]`.
An empty regex `""` means the entry is only shown in the lookup tab, never auto-detected.

## Sources

- HTTP: RFC 9110 - https://www.rfc-editor.org/rfc/rfc9110 / IANA registry - https://www.iana.org/assignments/http-status-codes
- EPP domain status: RFC 5731 - https://www.rfc-editor.org/rfc/rfc5731 / ICANN - https://www.icann.org/epp
- DNS RCODEs: RFC 1035 - https://www.rfc-editor.org/rfc/rfc1035
- Cloudflare 5xx: https://developers.cloudflare.com/support/troubleshooting/http-status-codes/cloudflare-5xx-errors/
- Discord: https://discord.com/developers/docs/topics/opcodes-and-status-codes
- errno: https://man7.org/linux/man-pages/man3/errno.3.html
