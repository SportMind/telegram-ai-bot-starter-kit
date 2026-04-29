# Example: Match Intelligence Bot — Supporter Group

> **Use case**: A Telegram group for an Arsenal supporter association
> who want match briefings, squad context, and rivalry intelligence
> delivered directly without visiting external sources.
> Config: `config/match-intelligence-bot.yaml`

---

## Scenario

The Highbury House supporter group has ~200 members. They want a bot that can:

1. Deliver a full pre-match briefing 90 minutes before kickoff (manual or scheduled)
2. Answer squad availability and form questions during the week
3. Provide rivalry context for specific opponents
4. Surface match conditions intelligence (venue, weather, travel factors)

---

## Setup

1. Clone the kit and open `config/match-intelligence-bot.yaml`
2. Fill in your bot token and LLM key
3. Add the group to `allowed_chat_ids` (or leave empty for open access)
4. Set `tone_addendum` to match your group's preferred language/style
5. **Deploy**: Use @LobsterClawBot (Path A) or deploy your own manager bot using any Bot API framework — see `config/bot-api-bootstrap.yaml`

---

## Interaction 1: Full pre-match briefing

**User in group:**
```
/prematch Arsenal vs Crystal Palace Premier League
```

**Bot response:**
```
Pre-Match Briefing
Arsenal vs Crystal Palace
Premier League · Emirates Stadium

Signal
Direction: HOME (76% confidence)

Key factors
• Arsenal's SMS reads 88 — elevated by title race proximity and
  consecutive clean sheets creating a positive defensive momentum cycle.
• Crystal Palace's SMS reads 64 — standard mid-table motivation;
  nothing structurally at stake for this fixture.
• AFS differential: Arsenal 74, Palace 51 — meaningful gap in recent
  output quality across key positions.
• Emirates home advantage (night game): historically adds ~4 points
  to Arsenal's underlying performance scores.

Watch for
• Bukayo Saka's first-half movement patterns — he has scored in 4
  of his last 5 home appearances.
• Palace's counter-attack setup: their SMS does not indicate
  overwhelming effort but they are technically disciplined.
• If Arsenal lead by 65 minutes, expect defensive consolidation —
  the manager will protect the result over performance.

SportMind · 2026-04-27
```

---

## Interaction 2: Squad form question

**User:**
```
/form Arsenal
```

**Bot response:**
```
Arsenal Squad Form
AFS: 74 / 100 — Active form band

Key positional readings
• Goalkeeper: Strong (AFS 79) — no form concerns
• Central defence: Strong (AFS 76) — settled pairing, minutes load normal
• Central midfield: Elevated (AFS 81) — currently the highest-output unit
• Attacking third: Good (AFS 71) — primary attacker slightly below peak

Flags
• No injury concerns from last squad session
• One player in contract year — monitor PS (Pressure Score) signal
  as transfer window approaches

Overall: Arsenal are in form. No AFS red zones.

SportMind · 2026-04-27
```

---

## Interaction 3: Rivalry context

**User:**
```
/rivalry Arsenal vs Tottenham
```

**Bot response:**
```
Rivalry Intelligence — Arsenal vs Tottenham

The North London Derby carries a SportMind rivalry multiplier of ×1.85
on standard SMS readings for both sides. This is among the highest
rivalry amplifiers in the English football domain.

What this means
• Both squads' SMS scores are elevated independent of league position
  or trophy stakes. The rivalry itself is the motivating factor.
• Standard form and availability signals are less predictive in
  derby contexts — historical upset rate is above average.
• Community activation (CHI) for $AFC fan token holders spikes
  significantly in the 72 hours surrounding a derby fixture.

Historical pattern
Arsenal's SMS profile in North London Derbies favours performances
above their season average when: (a) they are above Tottenham in
the table, and (b) the match falls in the second half of the season.
Current conditions: check current standings.

SportMind · rivalry context · 2026-04-27
```

---

## Interaction 4: Match conditions

**User:**
```
/conditions Emirates Stadium
```

**Bot response:**
```
Match Conditions — Emirates Stadium

Surface: Grass (hybrid). Current condition: good.
Roof: Open, covered stands. Wind exposure: moderate.

Relevant SportMind conditions context
• Emirates night games (KO 20:00 GMT+) show a consistent +3.2 point
  home advantage vs afternoon kickoffs in SportMind's calibration set.
• No dew factor applicable (indoor grass, drainage controlled).
• Late-season April conditions: typically firm pitch, fast surface.
  Favours technical passing styles over long-ball approaches.

No adverse conditions flags active.

SportMind · conditions context · 2026-04-27
```

---

## Customisations

- **Different club**: All team references and rivalry multipliers are derived from SportMind's `sports/football/` and `fan-token/clubs/` directories. Swap the club references in your prompts and configs.
- **Scheduled briefings**: Enable `scheduled_briefings: enabled: true` in the config and populate the fixture list. The bot will push a full `/prematch` briefing 90 minutes before kickoff automatically.
- **Language**: The `tone_addendum` field in the config lets you adjust the register. For a formal press-style channel, remove the conversational framing. For a casual group, you can instruct the bot to use informal language.
- **Competition filter**: Add a competition filter to only respond to `/prematch` commands for specific competitions (e.g., only UCL fixtures get full briefings; league matches get abbreviated versions).

---

## Known limitations

- The bot does not pull real-time team news or lineup announcements. It uses SportMind's modular reasoning framework — users should cross-reference confirmed team news before kickoff.
- Scheduled briefings require a cron job or scheduled task in your deployment environment. Implement using your framework's job scheduling, or a simple external cron pointing at your bot's API endpoint.
- Rivalry multipliers are calibrated for major rivalries in the SportMind library. For lower-league or regional rivalries, the bot will apply standard SMS without a rivalry modifier.
