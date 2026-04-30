# Changelog — SportMind Telegram AI Bot Starter Kit

## v1.3.0 — 2026-04-30

Website page updates: terminology corrections and data accuracy pass.

### Changed

**SportMind Suite section** (`telegram-ai-bot-starter-kit` website page)
- Section header renamed from "SportMind ecosystem" to "SportMind Suite"
- Body copy updated from "open sports intelligence ecosystem" to "open sports intelligence suite" — consistent with terminology used across the SportMind suite
- Skill file count updated from 456 to 594, reflecting current core library state
- Wallet Kit repository link corrected from `SportMind/wallet-kit` to `SportMind/fan-token-agentic-wallet-starter-kit`

---

## v1.2.0 — 2026-04-29

Introduced community-led governance. The project founder no longer reviews
or merges pull requests. All contributions are reviewed by Trusted Reviewers
drawn from the Founding Calibrator community.

### Added

**GOVERNANCE.md** — Defines roles (Contributor, Trusted Reviewer, Maintainer),
merge rules by PR type, the disagreement resolution process, and the amendment
process for governance changes. Trusted Reviewer status is earned via Founding
Calibrator status or 2+ merged PRs. Maintainers are promoted from Trusted
Reviewers after 90 days and 10+ reviews.

**.github/CODEOWNERS** — Routes PR review requests automatically based on
which files are changed. Prompts and configs require @SportMind/trusted-reviewers.
GOVERNANCE.md, CODEOWNERS, and LICENSE require @SportMind/maintainers.
Includes a setup checklist for configuring GitHub branch protection rules.

**CONTRIBUTING.md** — Rewritten to reflect community-led review. Documents
the review process, approval thresholds, and the path to becoming a Trusted
Reviewer. Removed all references to founder review.

### Changed

The founder role is now explicitly non-reviewing: [@pele-roberts](https://github.com/pele-roberts)
may contribute PRs like any other contributor, subject to the same review
process. Governance changes require Maintainer approval only.

---

## v1.1.0 — 2026-04-29

Corrected runtime references throughout the kit. v1.0.0 contained fabricated
tooling names (OpenClaw, @LobsterClawBot as a fictional product). This release
replaces all of those with accurate references to Telegram's real Managed Bots
platform and @LobsterClawBot as a real Telegram manager bot.

### What changed

**README.md** — Complete rewrite of the Quick Start and Architecture sections.
Added accurate description of how Telegram Managed Bots work, with the real
user flow (manager bot → native Telegram confirmation → child bot created →
"Its behaviour is defined by [manager bot]"). Added Path A (@LobsterClawBot)
and Path B (self-hosted manager bot) as the two real deployment paths.

**config/raw-bot-api-bootstrap.yaml** → renamed **config/bot-api-bootstrap.yaml**
— Rewritten as an accurate framework-agnostic skeleton. Documents the Managed
Bots architecture, pseudo-code implementation pattern, and links to four real
Bot API frameworks (python-telegram-bot, grammY, telegraf, aiogram).

**All configs** — Removed fictional `openclaw:` runtime blocks. Replaced with
an accurate `# ── DEPLOYMENT` section describing Path A (@LobsterClawBot) and
Path B (self-hosted, any framework) with correct documentation links.

**All examples** — Removed `openclaw deploy` commands. Replaced with accurate
deployment instructions referencing `config/bot-api-bootstrap.yaml`.

**CONTRIBUTING.md** — Removed `openclaw dev` test command. Replaced with
accurate local testing instruction (Bot API polling mode).

### What did not change

All prompts (`prompts/`) are unchanged — they are framework-agnostic and were
accurate in v1.0.0. All use case logic, SportMind metric references, signal
output formats, and example conversation flows are unchanged.

---

## v1.0.0 — 2026-04-27

Initial release. See CHANGELOG entry above for corrections applied in v1.1.0.

### Included in v1.0.0

- 5 use cases, 6 configs, 4 prompts, 3 complete examples
- Fan token trading bot with $AFC Arsenal FTP PATH_2 scenario
- Match intelligence bot for supporter groups
- Calibration bot with 3 storage backends (local JSON, GitHub PR, webhook)
- Sentiment monitor (CHI/TVS)
- Macro event interpreter (MiCA, SEC/CFTC, crypto cycle)
- MIT license
