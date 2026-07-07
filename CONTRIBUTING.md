# Contributing to HZLib

Thank you for considering a contribution to HZLib. This document covers everything you need to know before you start.

---

## Your Credit, Your Copyright

This is the most important thing to read first.

**When you contribute to HZLib, the copyright in your contribution stays with you.** Under LGPL v3, you grant the project a license to use your work — but you retain ownership. HZLib will not claim your code as its own.

Beyond the legal reality, every meaningful contribution is credited explicitly:

- Your name and GitHub handle are added to [`CONTRIBUTORS.md`](CONTRIBUTORS.md)
- The specific contribution is described — what you built, not just that you contributed
- If you designed a system or feature, that is noted as yours

This is a deliberate choice. People who put real work into this library deserve to have that work visible and attributed — not absorbed anonymously into a codebase.

---

## Before You Start

HZLib's API is not yet frozen. If you are planning a significant change — a new system, a refactor of an existing one, a new abstraction — please open an issue first and describe what you want to do. This prevents wasted effort if the direction conflicts with planned API work.

For bug fixes and documentation improvements, you can go straight to a pull request.

---

## Setting Up

```bash
git clone https://github.com/heria-zone/hzlib
cd hzlib/src/hzlib-1.21.1
```

**Requirements:**
- JDK 21
- Gradle (wrapper included — use `./gradlew`)

**Build:**
```bash
./gradlew build
```

**Build all loaders:**
```bash
./gradlew :hzlib-fabric:build
./gradlew :hzlib-forge:build
./gradlew :hzlib-neoforge:build
```

---

## Code Standards

HZLib follows the project-wide coding standards defined in:

[`docs/guidelines/Coding Style Enforcer.md`](../../docs/guidelines/Coding%20Style%20Enforcer.md)

The short version:
- One public class per file
- JavaDoc on all public API — focus on architectural role and why, not just what
- Section headers (`// -- Constants --`, `// -- Fields --`, etc.) to organise class structure
- Closing comments on closing braces: `} // methodName()`, `} // Class: ClassName`
- Interfaces prefixed with `I` (`IVariantFeature`, `IPlatformServices`)
- `Objects.requireNonNull` for parameter validation in public methods

If your PR introduces public API, it must have JavaDoc that explains the architectural role of the new class or method — not just what parameters it takes.

---

## Commit Messages

All commits must follow the project commit guidelines:

[`docs/guidelines/maintenance/GIT_COMMIT_GUIDELINES.md`](../../docs/guidelines/maintenance/GIT_COMMIT_GUIDELINES.md)

Quick reference:
```
ADD:   New feature, class, or significant code
FIX:   Bug fix
REF:   Refactor without behaviour change
REM:   Removal
DOCS:  Documentation only
CFG:   Build or configuration change
NULL:  Trivial formatting or whitespace
```

Format: `PREFIX: Brief imperative description under 50 characters`

---

## Opening an Issue

Use the issue templates — they exist to make sure bug reports contain the information needed to reproduce the problem. A bug report without a reproduction case will not be actionable.

For feature requests, lead with the use case, not the solution. "I want to do X but cannot because Y" is more useful than "please add Z".

---

## Opening a Pull Request

- One logical change per PR
- All three loaders must build without warnings
- If you are adding public API, update `CHANGELOG.md` with a brief entry under the next version
- Fill in the PR template — the checklist is there to help, not to bureaucratise

PRs that touch the public API surface will receive more scrutiny than internal refactors. That is expected — API changes have downstream impact on every mod that depends on HZLib.

---

## What Gets Accepted

**In scope for HZLib:**
- Entity framework improvements (features, variants, appearance)
- Animation profile system improvements
- NBT data pipeline improvements or new `DataType` entries
- Platform service improvements
- Bug fixes anywhere

**Out of scope for HZLib:**
- Robot-specific logic — that belongs in LovelyLib
- Mod-specific content — that belongs in the content mod
- GeckoLib rendering code — that belongs in HZLib: Animate (planned)

If you are unsure, open an issue first.

---

## Reporting a Security Issue

Do not open a public GitHub issue for security vulnerabilities.

See [`SECURITY.md`](SECURITY.md) for the private reporting process.

---

## Questions

Join the [Heria Zone Discord](https://discord.gg/KdZZMj89bU) — the `#dev` channel is the right place for questions about contributing or the architecture.
