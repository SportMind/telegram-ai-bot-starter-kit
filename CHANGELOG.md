# Changelog — SportMind Telegram AI Bot Starter Kit

## v1.4.0 — 2026-04-30

Full site and repository audit. All terminology, naming, responsive design,
navigation, and attribution issues resolved.

### Website — sportmind.github.io/telegram-ai-bot-starter-kit

**Navigation**
- Added Suite nav link
- Added hamburger menu for mobile with open/close toggle
- GitHub button now hidden on mobile (accessible via hamburger)
- Logo links correctly to sportmind.dev with breadcrumb display

**Hero**
- Removed badge line ("Telegram Managed Bots · MIT License · vX.X.X")
  from hero section — version references moved to footer only

**Suite section**
- Expanded from 3 to 4 repository cards — all SportMind suite members represented
- Added Fan Token Agentic Wallet Starter Kit with correct repository name
- Added SportMind MCP Server card
- Grid updated to 4-column layout (collapses to 2-column at 1024px, 1-column on mobile)
- Section anchor updated from `#ecosystem` to `#suite`

**Footer**
- Removed "Pele Roberts" from copyright line — now reads © 2026 SportMind
- Footer logo updated to show correct GitHub Pages URL with version
- SportMind link confirmed pointing to sportmind.dev
- All GitHub links verified correct

**Responsive and viewport**
- Added breakpoints for 1024px, 768px, 390px, and 375px
- All grids collapsing correctly at every breakpoint
- Minimum 44px touch targets applied to all buttons and nav elements
- Buttons stack vertically on mobile with full-width layout
- Hamburger/mobile menu opens and closes correctly
- Code blocks scrolling horizontally within container
- Footer wrapping correctly on mobile

**Meta**
- og:url and canonical updated to correct GitHub Pages URL
- Version updated to v1.4.0 in footer

### Repository — SportMind/telegram-ai-bot-starter-kit

**README.md**
- "open sports intelligence ecosystem" → "open sports intelligence suite"
- "Where this fits in the SportMind ecosystem" → "SportMind suite"
- `SportMind/wallet-kit` → `SportMind/fan-token-agentic-wallet-starter-kit`
- GitHub Pages URL added to links section

**LICENSE**
- "Copyright (c) 2026 SportMind — Pele Roberts" → "Copyright (c) 2026 SportMind"
- Name attribution is via git commit history only, not displayed in files

**GOVERNANCE.md**
- "created the SportMind ecosystem" → "created the SportMind suite"

---

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
