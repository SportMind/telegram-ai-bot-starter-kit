# Governance — SportMind Telegram AI Bot Starter Kit

This repository is governed by its contributor community. The project founder
([@pele-roberts](https://github.com/pele-roberts)) does not review or merge
pull requests. All contributions are reviewed and approved by community members
according to the process below.

---

## Guiding principle

The people best placed to judge a contribution to this kit are the people who
have already used it in production and contributed calibration records back to
the SportMind library. Domain knowledge and demonstrated honesty are the
qualification — not seniority or time served.

---

## Roles

### Contributor
Anyone who opens a pull request. No prior approval needed. See
[CONTRIBUTING.md](CONTRIBUTING.md) for what makes a good PR.

### Trusted Reviewer
A community member with review rights on pull requests. Trusted Reviewers are
listed in [CODEOWNERS](.github/CODEOWNERS) and in the
[Trusted Reviewers](#trusted-reviewers) section below.

Trusted Reviewers are drawn from two groups:

- **Founding Calibrators** — the first 10 external contributors to submit
  complete calibration records (prediction + outcome) to
  [SportMind/SportMind](https://github.com/SportMind/SportMind). These
  contributors have demonstrated they understand the SportMind framework and
  use it honestly.
- **Kit contributors with 2+ merged PRs** — anyone who has had two or more
  pull requests merged into this repository.

Trusted Reviewer status is offered, not applied for. Existing Trusted Reviewers
make the offer by opening an issue titled `Nominate: @username`.

### Maintainer
A Trusted Reviewer who has also been active for 90+ days and has reviewed 10+
PRs. Maintainers can merge pull requests once the review threshold is met.
Current maintainers are listed below.

---

## Merge rules

| PR type | Reviews required | Who can review |
|---|---|---|
| New use case (config + example) | 2 approvals | Any Trusted Reviewer |
| New or modified prompt | 2 approvals | Trusted Reviewer with calibration records in that sport/domain |
| Bug fix or docs update | 1 approval | Any Trusted Reviewer |
| New framework adapter | 1 approval | Any Trusted Reviewer |
| GOVERNANCE.md or CODEOWNERS change | 3 approvals | Maintainers only |

A PR author cannot approve their own PR.

Pull requests that have been open for **21 days** with no review activity are
eligible for merge with 1 approval if the PR meets all contribution standards
in [CONTRIBUTING.md](CONTRIBUTING.md). This prevents good work from stalling.

---

## What reviewers check

**For all PRs:**
- No real credentials committed (tokens, API keys, private endpoints)
- No dependencies requiring paid accounts
- Accurate references — no fabricated tools, platforms, or services
- `use_case_id` is unique and snake_case

**For prompts:**
- `## SportMind context` section declares all metrics and modifiers used
- Output format is specified
- Works with any OpenAI-compatible LLM (not model-specific)
- Claims about SportMind behaviour are consistent with the core library

**For configs:**
- All required fields present (see `config/fan-token-trading-bot.yaml`)
- `system_prompt_file` references a file that exists
- Placeholder values used for all credentials

**For examples:**
- At least one complete worked interaction shown
- `## Known limitations` section present and honest
- No `TODO` placeholders in critical fields

Reviewers are expected to test configs locally where practical. A review that
only checks formatting is not sufficient for prompts or new use cases.

---

## Disagreements

If two Trusted Reviewers disagree on a PR:

1. The reviewer who objects opens a comment explaining their specific concern.
2. A 7-day discussion period begins.
3. If unresolved, any Maintainer can call a simple majority vote among all
   Trusted Reviewers. Vote is open for 72 hours. Majority wins.

For GOVERNANCE.md or CODEOWNERS changes, the bar is higher: a two-thirds
majority of active Trusted Reviewers (those who have reviewed a PR in the
last 90 days).

---

## Trusted Reviewers

*This section is updated as Founding Calibrators are confirmed and kit
contributors reach 2 merged PRs.*

| Handle | Basis | Active since |
|---|---|---|
| *(awaiting first Founding Calibrators)* | | |

---

## Maintainers

| Handle | Since |
|---|---|
| *(promoted from Trusted Reviewers once criteria met)* | |

---

## Founder role

[@pele-roberts](https://github.com/pele-roberts) created the SportMind suite
and this kit. The founder role carries no special review or merge rights over
community contributions. The founder may contribute PRs like any other
contributor — subject to the same review process.

The founder retains the right to archive or transfer the repository, and to
update the LICENSE. All other governance decisions follow the process above.

---

## Amendments

Changes to this document require 3 Maintainer approvals and a 14-day comment
period announced in a GitHub Discussion. Any Trusted Reviewer may open an
amendment proposal.

---

*This governance model is inspired by the Apache meritocracy model and the
Rust project's RFC process, scaled to the size of this kit.*
