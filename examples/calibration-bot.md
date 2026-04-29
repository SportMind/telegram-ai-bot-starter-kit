# Example: Calibration Bot — Community Record Collection

> **Use case**: A public-facing Telegram bot that collects SportMind calibration
> records from the community and feeds them back into the SportMind calibration base.
> Config: `config/calibration-bot.yaml`

---

## What the calibration bot does

SportMind's accuracy claim (96% direction accuracy across 126 records) is built from submissions made before real events. The calibration bot makes it possible for anyone to:

1. Run SportMind before a real match or event
2. Submit their prediction through Telegram
3. Record the outcome after the event
4. Contribute to SportMind's growing calibration base

Wrong predictions are as valuable as correct ones. The goal is an honest, complete record — not a curated highlight reel.

The first 10 external contributors to submit complete records (prediction + outcome) earn Founding Calibrator status — permanently credited in the SportMind library's history.

---

## Setup

1. Clone the kit and open `config/calibration-bot.yaml`
2. Fill in your bot token and LLM key
3. Choose a storage backend: `local_json`, `github_pr`, or `webhook`
4. For GitHub PR backend: create a GitHub PAT with repo write access and set `storage.github.token`
5. **Deploy**: Use @LobsterClawBot (Path A) or deploy your own manager bot using any Bot API framework — see `config/bot-api-bootstrap.yaml`

---

## Full submission flow

### Step 1: Start

**User:**
```
/submit
```

**Bot response:**
```
SportMind Calibration Record

Let's record your prediction. I'll ask you a few questions.
You can type /cancel at any time to stop.

What sport is this prediction for?
(e.g. football, cricket, MMA, formula1, tennis)
```

**User:**
```
football
```

---

### Step 2: Event

**Bot:**
```
Name the event or match:
(e.g. Arsenal vs PSG · UCL semi-final · 2026-04-30)
```

**User:**
```
Arsenal vs Chelsea Premier League
```

---

### Step 3: Date

**Bot:**
```
When does/did it take place?
(date like 2026-05-03, or 'today', or 'tomorrow')
```

**User:**
```
2026-05-03
```

---

### Step 4: Direction

**Bot:**
```
Your prediction direction:
HOME / AWAY / DRAW / OVER / UNDER / YES / NO
```

**User:**
```
HOME
```

---

### Step 5: Confidence

**Bot:**
```
Confidence percentage? (50–100)
Higher = more certain. 50 = you're guessing.
```

**User:**
```
72
```

---

### Step 6: Modules used

**Bot:**
```
Which SportMind modules or context did you use?
(e.g. SMS, dew_factor, FTP PATH_2, rivalry multiplier, AFS)
```

**User:**
```
SMS, AFS, home advantage, no macro override
```

---

### Step 7: Notes (optional)

**Bot:**
```
Any notes on your reasoning? (optional)
Press /skip to skip.
```

**User:**
```
Arsenal have 3 consecutive clean sheets, Chelsea missing key midfielder.
SMS elevated by title race context.
```

---

### Confirmation

**Bot:**
```
Submission recorded ✓

Record ID: `SM-EXT-00047`
Sport: football
Event: Arsenal vs Chelsea · Premier League
Date: 2026-05-03
Direction: HOME
Confidence: 72%
Modules used: SMS, AFS, home advantage
Notes: Arsenal have 3 consecutive clean sheets...

Use /outcome SM-EXT-00047 when you know the result.
Wrong predictions count — submit all outcomes honestly.

SportMind First Record Challenge: you are record #3 of the first 10.
7 slots remaining for Founding Calibrator status.
https://github.com/SportMind/SportMind/blob/main/FIRST-RECORD-CHALLENGE.md
```

---

## Recording an outcome

After the match:

**User:**
```
/outcome SM-EXT-00047
```

**Bot:**
```
Record ID: SM-EXT-00047
Your prediction: HOME (Arsenal)
Match: Arsenal vs Chelsea · 2026-05-03

What was the actual outcome?
HOME / AWAY / DRAW / POSTPONED / VOID
```

**User:**
```
HOME
```

**Bot:**
```
Outcome recorded ✓

Record SM-EXT-00047 — CORRECT ✓
Your prediction: HOME
Actual result: HOME (Arsenal win)
Confidence declared: 72%

Your calibration record: 3 submitted, 2 outcomes recorded, 2/2 correct.
Accuracy so far: 100%

This record will be reviewed for inclusion in SportMind's calibration base.
Thank you for contributing.
```

---

## Leaderboard

**User:**
```
/leaderboard
```

**Bot:**
```
Top Calibrators — Last 30 days

1. @contributor_a — 12 records, 11/12 correct (91.7%)
2. @contributor_b — 8 records, 7/8 correct (87.5%)
3. @contributor_c — 7 records, 6/7 correct (85.7%)
4. @contributor_d — 5 records, 5/5 correct (100%)
5. @contributor_e — 4 records, 3/4 correct (75.0%)

Min 3 records required to appear. Wrong predictions count.
Submit yours: /submit

SportMind Calibration Base · 2026-04-27
```

---

## Storage backends

### local_json (default)
Records are written to `./data/calibration-records.json`. Simplest setup. No external dependencies. Manual export required to submit to SportMind.

```json
{
  "record_id": "SM-EXT-00047",
  "sport": "football",
  "event": "Arsenal vs Chelsea · Premier League",
  "event_date": "2026-05-03",
  "prediction_direction": "HOME",
  "confidence_pct": 72,
  "sportmind_modules_used": ["SMS", "AFS", "home_advantage"],
  "key_modifiers": ["SMS", "AFS"],
  "outcome": "HOME",
  "correct": true,
  "submitted_at": "2026-04-27T14:32:00Z",
  "outcome_recorded_at": "2026-05-03T22:15:00Z",
  "contributor_telegram_id": "HASHED_ID",
  "notes": "Arsenal have 3 consecutive clean sheets..."
}
```

### github_pr
Records are automatically submitted as pull requests to `SportMind/SportMind` on the `calibration-intake` branch. Enables direct contribution to the library without manual export.

Requires: GitHub PAT with `repo` write scope. Set in `config/calibration-bot.yaml` → `storage.github.token`.

### webhook
Records are POST'd to your endpoint as JSON. Use this to integrate with your own database or analytics pipeline.

---

## Customisations

- **Community-specific records**: If you are running the bot for a specific sport community (e.g., only cricket calibration), restrict the sport options in Step 1 to focus collection.
- **Module validation**: The bot currently accepts any free-text module description. To enforce SportMind module names, update the extraction prompt in the config to validate against the canonical module list.
- **Founding Calibrator tracking**: The `first_record_challenge.target_count` field controls when the Founding Calibrator congratulation message is sent. Set to a higher number if you want to extend the challenge window.

---

## Known limitations

- The bot collects predictions and outcomes but does not independently verify results. Outcome honesty depends on the contributor. This is intentional — the SportMind calibration methodology relies on self-reported outcomes submitted in good faith.
- Telegram user IDs are hashed before storage (when `log_user_ids: true`). The leaderboard uses Telegram display names, which can change. For persistent leaderboard tracking, consider a username-to-ID mapping layer.
- The GitHub PR backend creates one PR per record. For high-volume deployments, consider batching records into daily PR submissions via a cron job to avoid PR spam.
