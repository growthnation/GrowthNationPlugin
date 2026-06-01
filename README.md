![GrowthNation](assets/logo.svg)

# GrowthNation — Proof skills for AI agents

Two self-contained social-proof skills for B2B sales, in one plugin:

- **`/proof-audit`** — grade how fresh a company's testimonials, case studies, and reviews are, and get a concrete refresh list.
- **`/proof-meeting-prep`** — walk into a call knowing every person in the room, with the one proof angle that lands for each of them.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

---

## What's in here

| Command | What it does |
|---|---|
| **`/proof-audit`** | Point it at a domain — it finds the social proof on the site (testimonials, case studies, reviews, logo walls, customer stats), scores how **fresh** each piece is on a five-band scale (🟢 **Fresh** → ⚫ **Expired**), and prints a worst-first audit with prioritised refresh recommendations. Stale proof reads as neglect and quietly kills deals; this tells you what to fix. |
| **`/proof-meeting-prep`** | Give it the company, the people on the call, and what you're selling. It researches each person from public sources, works out what that role cares about and what they'll push back on, proposes the **single proof angle most likely to move them**, then reads the room (champion, buyer, gatekeeper, sequencing). |

**Self-contained:** both skills use only the agent's built-in **web search + fetch**. No API keys, no database, no CRM, no login — anyone can install and run them.

---

## Install

### Claude Code Terminal

```bash
/plugin marketplace add growthnation/GrowthNationPlugin
/plugin install growthnation@growthnation
/reload-plugins
```

Then use `/proof-audit` and `/proof-meeting-prep`.

**Optional — enable auto-update:** `/plugin`, then choose `Marketplaces` tab > `growthnation` > `Enable auto-update`

### Claude Cowork / Code Desktop

1. `Customize` > `Personal Plugins` > `+` > `Create Plugin` > `Add marketplace`, input `growthnation/GrowthNationPlugin`, click `Sync`
2. `Plugins` > `Personal` > `growthnation`, click `+` on `growthnation`
3. (**Claude Cowork only**) Enable web access: `Profile` (bottom left) > `Settings` > `Capabilities` > `Code execution and file creation` > turn on `Allow network egress`, then set `Domain allowlist` to `All domains` (the skills fetch arbitrary company and LinkedIn pages).

### Claude Chat Desktop

Each skill installs as its own ZIP:

1. Download the [Proof Audit ZIP](https://github.com/growthnation/GrowthNationPlugin/releases/download/latest/proof-audit-skill.zip) and/or the [Proof Meeting Prep ZIP](https://github.com/growthnation/GrowthNationPlugin/releases/download/latest/proof-meeting-prep-skill.zip)
2. In the app: `Customize` > `Skills` > `+` > `Create Skill` > `Upload a skill` (repeat per ZIP)
3. Enable web access: `Profile` (bottom left) > `Settings` > `Capabilities` > `Code execution and file creation` > turn on `Allow network egress`, then set `Domain allowlist` to `All domains`.

### Other Agents (Codex / Cursor / etc.)

Copy the skill folder(s) into your agent's skills directory:

```bash
cp -r plugins/growthnation/skills/proof-audit ~/.claude/skills/          # or your agent's equivalent
cp -r plugins/growthnation/skills/proof-meeting-prep ~/.claude/skills/
```

Or follow your agent's skill installation instructions to install manually.

---

## Optional: the GrowthNation connector

Installing the plugin also makes the **GrowthNation MCP connector** (`https://app.growthnation.ai/mcp`) available — but the two skills never depend on it. They stay fully self-contained: `/proof-audit` and `/proof-meeting-prep` run for anyone with nothing but web search + fetch.

The connector is a pure **add-on for GrowthNation users**: when it's connected, you can push results into your GrowthNation workspace (save discovered proof to the Customer Voice library, turn a meeting-prep brief into tailored Sparks, etc.) instead of just reading the markdown. Skip it and the skills lose nothing.

Your agent prompts for consent before the connector runs, and GrowthNation features behind it require a logged-in account.

---

## Usage

**Proof Audit**

- `/proof-audit acme.com` to run an audit on a domain.
- Or just describe the goal — *"how fresh is the proof on acme.org?"* — and the agent loads the skill via semantic matching.

> *"Run a proof audit on acme.org"* — discovers their case-study library and reviews, flags that the pages are undated, and recommends dating them.

**Proof Meeting Prep**

- `/proof-meeting-prep` then paste the deal — company, the people on the call, what you're selling.
- Or just describe it — *"I've got a call with Acme's CFO and VP Eng tomorrow about our CRM tool, what proof lands for each?"*

> *"Call with Acme tomorrow — CFO, VP Sales, and a RevOps lead. Selling a CRM-native proof tool, ~$40k, new logo."* — returns a brief per person (priorities, objections, proof angle, opener) and a room read with proof sequencing.

---

## How they work

**Proof Audit** reads each piece of proof for **staleness signals** — explicit dates, implicit date language ("during the pandemic"), image-URL date stamps (`/202405/`), copyright footers, tenure mentions, and product-version drift — and maps them to a 0–100 freshness score via a half-life heuristic (~6mo ≈ 90, 1yr ≈ 75, 2yr ≈ 50, 3yr ≈ 35, 4yr+ ≈ 20), then to a band:

| Score | Band | Read |
|---|---|---|
| 80–100 | 🟢 Fresh | Within ~the last year. |
| 60–79 | 🟡 Recent | ~1–2 years. Aging. |
| 40–59 | 🟠 Aging | ~2–3 years, or undated. |
| 20–39 | 🔴 Stale | ~3–4 years. Neglected. |
| 0–19 | ⚫ Expired | 4+ years or superseded. |

Undated proof scores 50 at low confidence — *unknown*, not automatically stale, but flagged because a buyer can't tell how old it is.

**Proof Meeting Prep** runs four reads per person — role priorities, likely objections, the one proof angle that wins (from a seven-type taxonomy: peer proof, hard ROI, authority, risk/trust, reciprocity, champion enablement, identity), and an opener — then reads the room and sequences the proof. Every claim is labelled **`[cited]`** (source named) or **`[inferred]`** (reasoned from role × industry × stage). It never invents a quote, a customer name, or a biographical detail.

---

## License

[MIT](LICENSE) — GrowthNation
