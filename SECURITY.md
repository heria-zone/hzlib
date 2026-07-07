# Security Policy — HZLib

## Reporting a Vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

If you find something, tell me privately and I'll fix it. That's all this is.

### Primary channel — GitHub Private Vulnerability Reporting

Go to the [Security tab](../../security) of this repository and click **"Report a vulnerability"**. GitHub creates a private draft between you and the maintainer. No public exposure, no email required.

### Secondary channel — Discord

If you prefer, send a direct message to **MSymbios** on the [Heria Zone Discord](https://discord.gg/KdZZMj89bU).

---

## What Counts as a Security Issue

HZLib is a Minecraft mod library. The realistic threat surface is narrow but real:

- **Crash exploits** — malformed NBT data or crafted input that crashes a server or client
- **Save corruption** — behaviour in the data pipeline or migration chain that silently destroys player data
- **Duplication bugs** — item or entity data duplication exploitable on multiplayer servers
- **Arbitrary code execution** — anything that allows running unexpected code through the library

If you are unsure whether something qualifies, report it privately anyway. Better a false alarm than a public disclosure.

## What Does NOT Belong Here

- General bugs → open a [GitHub Issue](../../issues)
- Feature requests → open a [GitHub Issue](../../issues)
- Usage questions → join [Discord](https://discord.gg/KdZZMj89bU) `#dev`

---

## What to Include in a Report

The more detail, the faster the fix:

- Description of the vulnerability and its impact
- Steps to reproduce (minimal reproduction case if possible)
- HZLib version and Minecraft version
- Loader (Fabric / Forge / NeoForge)
- Any relevant code snippets or crash logs

---

## What to Expect

- **Acknowledgement** — within 48 hours of receipt
- **Initial assessment** — within 1 week
- **Fix timeline** — depends on severity and complexity; critical issues are prioritised
- **Credit** — if you want to be credited for the find, say so in your report and I will include your name in the fix notes

This is a solo project. Response times reflect that — I will always acknowledge and act, but I am one person.

---

## Supported Versions

| Version | Supported |
|---|---|
| Latest release | ✅ |
| Older releases | ⚠️ Best effort — critical fixes only |
