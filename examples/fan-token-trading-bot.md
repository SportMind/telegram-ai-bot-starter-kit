# Example: Fan Token Trading Bot — $AFC Arsenal FTP PATH_2

> **Use case**: A private Telegram channel for a group of $AFC Arsenal fan token holders
> who want SportMind intelligence delivered directly into their existing discussion space.
> Config: `config/fan-token-trading-bot.yaml`

---

## Scenario

Arsenal are playing PSG in a UCL knockout match. The channel members want:

1. A pre-match signal before kickoff
2. FTP PATH_2 interpretation (will this be a supply reduction or expansion event?)
3. Community sentiment context leading into the match
4. A price movement attribution after the match

This example walks through each of those four interactions as they would appear in Telegram.

---

## Setup

1. Clone the kit and open `config/fan-token-trading-bot.yaml`
2. Fill in your bot token and LLM key
3. Set `allowed_chat_ids` to your private channel ID
4. Set `sportmind_context.base_path` to your local SportMind library path
5. **Deploy**: Use @LobsterClawBot (Path A) or deploy your own manager bot using any Bot API framework — see `config/bot-api-bootstrap.yaml`

---

## Interaction 1: Pre-match signal

**User in channel:**
```
/signal Arsenal vs PSG UCL semi-final second leg
```

**Bot response:**
```
SportMind Signal

{
  "direction": "HOME",
  "adjusted_score": 71.2,
  "sms": 82,
  "recommended_action": "ENTER",
  "composite_modifier": 1.14,
  "modifiers_applied": {
    "athlete_modifier": 1.10,
    "macro_modifier": 1.00
  },
  "flags": {
    "lineup_unconfirmed": false,
    "macro_override_active": false,
    "ftp_path2_active": true,
    "supply_event_type": "REDUCTION"
  }
}

Analysis
Arsenal carry a 1-0 aggregate lead into this second leg at the Emirates,
creating a structural asymmetry: they can play for the draw. SMS reads 82
— elevated by trophy proximity (UCL final within reach), home advantage,
and confirmed full-strength squad. PSG must attack, which plays to
Arsenal's defensive transition strengths.

FTP PATH_2 is active. A HOME WIN result triggers a $AFC supply reduction
event. The competitive signal and the tokenomics consequence align.

Active flags
⚠️ ftp_path2_active: true — supply reduction event predicted on WIN
⚠️ lineup_unconfirmed: false — starting XI confirmed

SportMind · pre-match signal · v1.0.0
```

---

## Interaction 2: FTP PATH_2 status

**User:**
```
/ftp $AFC
```

**Bot response:**
```
FTP PATH_2 Status — $AFC (Arsenal)

Phase: PATH_2 ACTIVE
Supply event type: WIN-TRIGGERED REDUCTION
Last trigger: [most recent match result]

Interpretation
$AFC runs a performance-linked supply mechanism on the Chiliz Chain.
When Arsenal WIN, tokens are burned — reducing circulating supply.
When Arsenal LOSE, tokens are minted — expanding supply.
This match (UCL semi-final 2nd leg) is a PATH_2-eligible fixture.

Current prediction: SUPPLY REDUCTION EVENT (WIN signal active)

SportMind · 2026-04-27
```

---

## Interaction 3: Sentiment check

**User:**
```
/sentiment $AFC
```

**Bot response:**
```
Community Sentiment — $AFC

CHI: 78 / 100 — Peak engagement band
TVS: 62 / 100 — Elevated circulation
Divergence: none — CHI and TVS confirm each other

Overall sentiment: POSITIVE

The community is in a high-activation state consistent with UCL
knockout proximity. Governance participation is elevated; fan vote
activity on match-day content has spiked in the 48 hours pre-match.
TVS elevation suggests some pre-match token movement but not unusual
volume for a UCL semi-final context.

Flags: none active

SportMind · 2026-04-27
```

---

## Interaction 4: Post-match attribution

Arsenal win 2-1. The $AFC token rises 8% within 2 hours of the final whistle.

**User:**
```
$AFC up 8% in 2hrs after the win — what drove it?
```

**Bot response:**
```
Price movement attribution

Token: $AFC
Movement: +8% over 2 hours post-match

Primary cause
Layer: FTP PATH_2 — Supply event
Arsenal WIN triggered a supply reduction (burn) event on the Chiliz Chain.
Reduced circulating supply creates direct price support. This is the
dominant driver — a mechanism-level price catalyst, not purely sentiment.

Secondary causes
- CHI shift: Community health spiked from 78 to 91 post-win, converting
  high pre-match engagement into sustained post-match activity.
- Crypto cycle amplification: Broadly positive altcoin conditions
  amplified the magnitude of the sport-driven move.

Anomalies
None — all SportMind modifier layers aligned in the positive direction.
This is a high-conviction, well-attributed move.

Confidence in attribution
HIGH — FTP PATH_2 is a confirmed on-chain mechanism; the supply event
is verifiable on-chain independent of price analysis.

SportMind modifier stack · v1.0.0
```

---

## Customisations

This example uses the default Arsenal scenario. To adapt:

- **Different club**: Change the token references and update `sportmind_context` to load the relevant club's fan token file from `SportMind/SportMind/fan-token/clubs/`.
- **Different competition**: UCL knockout dynamics differ from league games (higher SMS, higher public attention). For league matches, expect lower SMS readings and smaller TVS spikes.
- **Multiple tokens**: The bot handles one token per command by default. To monitor multiple tokens simultaneously, deploy separate bot instances with separate configs, or extend the routing logic in your framework adapter.

---

## Known limitations

- FTP PATH_2 mechanics are specific to $AFC Arsenal and other clubs with confirmed PATH_2 configs. Verify whether your target club has an active PATH_2 before using the supply event interpretation.
- SMS estimates are generated from the SportMind framework, not real-time data feeds. Lineup confirmation, injury news, and press conference signals should be checked manually before high-stakes decisions.
- The bot does not have access to real-time price data unless integrated with an external price feed. Post-match attribution is most accurate when the user provides the observed movement.
