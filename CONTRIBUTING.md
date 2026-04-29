# Contributing to SportMind Telegram AI Bot Starter Kit

Contributions are reviewed and merged by the community — not the project
founder. Before you open a PR, read [GOVERNANCE.md](GOVERNANCE.md) to
understand who reviews what and how decisions are made.

---

## What the community wants

The highest-value contributions are:

1. **New use case configs** — a working `config/` + `examples/` pair for a use case not yet covered
2. **Prompt refinements** — improvements to existing prompts in `prompts/` backed by real deployment evidence
3. **Framework adapters** — config templates for additional Bot API frameworks (grammY, python-telegram-bot, telegraf, aiogram)
4. **Calibration bot records** — actual calibration submissions collected by a deployed `calibration-bot` instance

A working config with honest limitations is more valuable than a polished one that only works in one scenario.

---

## How to contribute

### Fork a use case

1. Fork this repository
2. Copy the closest existing config: `cp config/fan-token-trading-bot.yaml config/my-use-case.yaml`
3. Copy the closest example: `cp examples/fan-token-trading-bot.md examples/my-use-case.md`
4. Edit both to match your use case
5. Test locally using your Bot API framework of choice in polling mode
6. Add a `## Customisations` section to your example documenting what you changed
7. Open a pull request against `main`

### Refine a prompt

1. Copy the relevant prompt: `cp prompts/pre-match-signal.md prompts/my-prompt.md`
2. Make your changes
3. In your PR, state which SportMind metrics or modifiers your version depends on
4. Include any deployment evidence you have — even 5 real test runs is useful

### Add a framework adapter

1. Create `config/adapters/YOUR-FRAMEWORK.yaml` with a minimal working bootstrap
2. Document it in `examples/` or a new `ADAPTERS.md`
3. Note Bot API version compatibility

---

## Contribution standards

Reviewers check these before approving. Save yourself a round-trip by checking
them before you open a PR.

### All PRs
- No real credentials — tokens, API keys, or private endpoints must use placeholder values
- No dependencies requiring paid accounts. The kit must remain zero-cost to deploy.
- No fabricated tools, platforms, or services. If you're unsure whether something
  is real, check before including it.

### Configs
- All required fields present (see `config/fan-token-trading-bot.yaml`)
- `system_prompt_file` references a file that actually exists in `prompts/`
- `use_case_id` is unique and snake_case

### Prompts
- `## SportMind context` section at the top declaring all metrics and modifiers used
- Output format specified (JSON schema or structured markdown)
- Works with any OpenAI-compatible LLM — not tied to a specific model

### Examples
- At least one complete worked interaction (user message → bot response)
- `## Known limitations` section — honest about what doesn't work or isn't tested
- No `TODO` placeholders in critical fields

---

## Submitting a new use case

When opening a PR for a new use case, include:

1. `config/YOUR-USE-CASE.yaml` + `examples/YOUR-USE-CASE.md`
2. If a new prompt is needed: `prompts/YOUR-PROMPT.md`
3. An update to the use case table in `README.md`
4. In the PR description: how you tested it, which LLM, how many messages, any edge cases

PRs without a working config won't be merged, but will be listed in
`PENDING-USE-CASES.md` so the community can pick them up.

---

## Submitting calibration data

If you've deployed the `calibration-bot` and collected records:

1. Format records per `SportMind/SportMind` → `calibration/SUBMISSION-FORMAT.md`
2. Open a PR against **`SportMind/SportMind`** (the core library), not this kit
3. Reference this kit in your PR so the submission source is credited

Submitting 10+ records makes you eligible for Founding Calibrator status —
which also earns you Trusted Reviewer rights in this kit. See [GOVERNANCE.md](GOVERNANCE.md).

---

## The review process

Pull requests are reviewed by Trusted Reviewers — community members who are
Founding Calibrators or have 2+ merged PRs in this kit. The founder does not
review contributions.

- **New use cases and prompts**: 2 approvals required
- **Bug fixes and docs**: 1 approval required
- **GOVERNANCE.md or CODEOWNERS**: 3 Maintainer approvals required

PRs open for 21 days with no review activity are eligible for merge with
1 approval if they meet all standards above. Good work doesn't stall.

Full details in [GOVERNANCE.md](GOVERNANCE.md).

---

## Becoming a Trusted Reviewer

You don't apply — you get nominated by an existing Trusted Reviewer once you
meet one of these criteria:

- You are a confirmed Founding Calibrator in `SportMind/SportMind`
- You have 2+ merged PRs in this kit

Nominations are opened as a GitHub issue: `Nominate: @username`.

---

## Code of conduct

- Be specific. Vague issues and PRs without reproduction steps will be closed.
- Credit the SportMind library when you fork use cases publicly.
- Reviews should assess substance, not style. Disagree on the specifics.

---

Questions? Open a GitHub Discussion on [SportMind/SportMind](https://github.com/SportMind/SportMind).
