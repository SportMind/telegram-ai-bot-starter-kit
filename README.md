# SportMind Telegram AI Bot Starter Kit

> **A standalone starter kit for deploying SportMind-powered AI agent bots on Telegram in minutes.**  
> Part of the [SportMind](https://github.com/SportMind/SportMind) open sports intelligence ecosystem.

---

## What this is

The SportMind Telegram AI Bot Starter Kit gives developers a ready-made bridge between SportMind's sports intelligence layer and Telegram's **Managed Bots** platform.

Using Telegram's native [Managed Bots](https://core.telegram.org/bots/features#managed-bots) feature, a **manager bot** (like [@LobsterClawBot](https://t.me/LobsterClawBot)) creates and manages child bots on behalf of users — each one a personal AI agent with its own username, its own chat, and its own behaviour defined entirely by your SportMind prompt. Users never touch BotFather. They tap **Create a New Bot** inside the manager bot and their agent is live in seconds.

This kit provides the prompts, configs, and examples to define what those AI agents know and how they behave — using SportMind as the intelligence layer.

---

## How Telegram Managed Bots work

This is a real, documented Telegram platform feature. The user flow:

```
1. User opens a manager bot (e.g. @LobsterClawBot — "LobsterFather")
2. Manager bot presents: "Create your personal AI agent"
3. User taps "Create a New Bot"
4. Telegram shows a native system confirmation:
     "LobsterClawBot would like to create and manage
      a chatbot on your behalf."
     Bot name:     AI Agent #007
     Bot username: @TeleClaw007bot
5. User taps "Create" — Telegram creates the child bot natively
6. Confirmation: "AI Agent #007 is ready!
                  Its behaviour is defined by LobsterClawBot."
7. User taps Start → child bot responds as a fully live AI agent
```

The manager bot controls the child bot's behaviour. The child bot's intelligence — what it knows, how it reasons — is defined by the system prompt you load into it. **That's what this kit provides.**

Reference: [Telegram Managed Bots — core.telegram.org](https://core.telegram.org/bots/features#managed-bots)

---

## Where this fits in the SportMind ecosystem

```
SportMind/SportMind               ← Core intelligence library (42 sports, 5 layers)
SportMind/wallet-kit              ← Chiliz Chain on-chain integration
SportMind/telegram-ai-bot-starter-kit  ← This repository
```

The starter kit references the `telegram/` layer of `SportMind/SportMind` for intelligence context. Each prompt is self-contained enough to work standalone, but significantly more powerful when loaded with SportMind context files.

---

## Quick start

### Path A — Use @LobsterClawBot as your manager bot (fastest)

[@LobsterClawBot](https://t.me/LobsterClawBot) is a Telegram Managed Bots manager. It handles all bot creation and routing. You define what your agent knows by configuring the system prompt.

1. Open [@LobsterClawBot](https://t.me/LobsterClawBot) on Telegram
2. Tap **Create a New Bot**
3. Confirm the native Telegram prompt (bot name + username auto-suggested)
4. Your agent is live — configure it with a SportMind prompt from `prompts/`

To use SportMind prompts as the intelligence layer, load a prompt from `prompts/` as your agent's system message via LobsterClawBot's configuration interface.

### Path B — Build your own manager bot

Full control — your own branding, your own Mini App, your own routing logic.

1. **Create your manager bot** via [@BotFather](https://t.me/botfather)
2. **Enable Managed Bots** for your manager bot in BotFather settings
3. **Get an LLM key** — any OpenAI-compatible endpoint works
4. **Load a system prompt** from `prompts/` as your agent's intelligence layer
5. **Deploy** using any Bot API framework — see `config/bot-api-bootstrap.yaml` for a framework-agnostic skeleton

Reference: [Creating your own management bot](https://core.telegram.org/bots/features#creating-your-own-management-bot)

---

## Use cases

| Use case | Config | Example | Description |
|---|---|---|---|
| Fan token trading bot | `config/fan-token-trading-bot.yaml` | `examples/fan-token-trading-bot.md` | Fan token signals, FTP PATH_2, supply events |
| Match intelligence bot | `config/match-intelligence-bot.yaml` | `examples/match-intelligence-bot.md` | Pre-match briefings for supporter groups |
| Calibration bot | `config/calibration-bot.yaml` | `examples/calibration-bot.md` | Collect calibration records from community |
| Sentiment monitor | `config/sentiment-monitor.yaml` | — | Group sentiment tracking (CHI/TVS) |
| Macro event interpreter | `config/macro-event-interpreter.yaml` | — | Regulatory and cycle event framing |

---

## Prompts

The `prompts/` directory contains pre-built system prompts, each pre-loaded with the SportMind context variables they depend on. Load these as the **system message** in your LLM call — they define the agent's intelligence and reasoning behaviour.

| Prompt | SportMind context | Purpose |
|---|---|---|
| `sentiment-monitor.md` | CHI, TVS | Fan community sentiment analysis |
| `pre-match-signal.md` | SMS, FTP PATH_2 | Pre-match front-running signal |
| `price-movement-explainer.md` | All modifiers | Cause attribution reasoning |
| `macro-event-interpreter.md` | Macro layer, regulatory | Regulatory and crypto cycle events |

---

## Architecture

### Managed Bots model (Path A)

```
User taps "Create a New Bot" in manager bot
        ↓
Telegram native confirmation → child bot created with own username
        ↓
User messages child bot
        ↓
Manager bot receives update, routes to LLM
        ↓
System prompt (from prompts/) + SportMind context files
        ↓
LLM (your key, your model — any OpenAI-compatible endpoint)
        ↓
Structured SportMind output → Telegram reply
```

### Self-hosted manager bot (Path B)

```
Your manager bot (standard Telegram Bot API)
        ↓
Creates child bots via Managed Bots API
        ↓
Receives all child bot messages via bot-to-bot routing
        ↓
System prompt (from prompts/) + SportMind context files
        ↓
LLM → Structured output → Telegram reply
```

The kit never calls SportMind's servers. All intelligence is loaded from markdown files. The LLM is the only external runtime dependency.

---

## SportMind intelligence layer

Key metrics referenced across the kit's prompts:

| Metric | Layer | Used in |
|---|---|---|
| SMS (Squad Motivation Score) | Athlete | pre-match-signal, match-intelligence-bot |
| CHI (Community Health Index) | Fan Token | sentiment-monitor, fan-token-trading-bot |
| TVS (Token Velocity Score) | Fan Token | sentiment-monitor, fan-token-trading-bot |
| FTP PATH_2 | Fan Token | fan-token-trading-bot |
| AFS (Athlete Form Score) | Athlete | pre-match-signal |
| PS (Pressure Score) | Athlete | pre-match-signal |

Full metric definitions: `SportMind/SportMind` → `core/composite-metrics.md`

---

## Repository structure

```
telegram-ai-bot-starter-kit/
├── README.md
├── CONTRIBUTING.md
├── LICENSE
├── CHANGELOG.md
├── config/
│   ├── bot-api-bootstrap.yaml       ← framework-agnostic skeleton
│   ├── fan-token-trading-bot.yaml
│   ├── match-intelligence-bot.yaml
│   ├── calibration-bot.yaml
│   ├── sentiment-monitor.yaml
│   └── macro-event-interpreter.yaml
├── prompts/
│   ├── pre-match-signal.md
│   ├── sentiment-monitor.md
│   ├── price-movement-explainer.md
│   └── macro-event-interpreter.md
└── examples/
    ├── fan-token-trading-bot.md
    ├── match-intelligence-bot.md
    └── calibration-bot.md
```

---

## License

MIT — see [LICENSE](LICENSE). Free to use, fork, and deploy commercially.

---

## Links

- [SportMind core library](https://github.com/SportMind/SportMind)
- [SportMind website](https://sportmind.dev)
- [Telegram Managed Bots documentation](https://core.telegram.org/bots/features#managed-bots)
- [Telegram Bot API reference](https://core.telegram.org/bots/api)
- [@LobsterClawBot on Telegram](https://t.me/LobsterClawBot)
- [First Record Challenge](https://github.com/SportMind/SportMind/blob/main/FIRST-RECORD-CHALLENGE.md)
