![GrowthNation](assets/logo.svg)

# GrowthNation — Proof skills for AI agents

Five self-contained social-proof skills for B2B sales, in one plugin:

- **`/proof-audit`** — grade how fresh a company's testimonials, case studies, and reviews are, and get a concrete refresh list.
- **`/proof-meeting-prep`** — walk into a call knowing every person in the room, with the one proof angle that lands for each of them.
- **`/proof-email`** — write a cold or warm sales email to a specific person, grounded in real proof and one influence principle.
- **`/proof-dm`** — write a short LinkedIn DM (≤80 words) that earns a reply.
- **`/proof-post`** — write a public LinkedIn post that pulls inbound, tuned to an audience.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

---

## What's in here

| Command | What it does |
|---|---|
| **`/proof-audit`** | Point it at a domain — it finds the social proof on the site (testimonials, case studies, reviews, logo walls, customer stats), scores how **fresh** each piece is on a five-band scale (🟢 **Fresh** → ⚫ **Expired**), and prints a worst-first audit with prioritised refresh recommendations. Stale proof reads as neglect and quietly kills deals; this tells you what to fix. |
| **`/proof-meeting-prep`** | Give it the company, the people on the call, and what you're selling. It researches each person from public sources, works out what that role cares about and what they'll push back on, proposes the **single proof angle most likely to move them**, then reads the room (champion, buyer, gatekeeper, sequencing). |
| **`/proof-email`** | Give it the recipient (name + role + company) and what you're selling — it pulls the right proof and writes a ready-to-send **subject + body**, tailored to the recipient's role and built on one influence principle, with the reason it works. |
| **`/proof-dm`** | Same, for a **LinkedIn DM** — body only, ≤80 words, one sharp proof point, one frictionless ask. Ready to paste. |
| **`/proof-post`** | Give it a topic + audience — it writes a public **LinkedIn post** (hook + short paras + soft CTA, ≤1200 chars) grounded in a real customer win and the angle that resonates with that audience. |

**Standalone by default:** every skill runs on the agent's built-in **web search + fetch** — no API keys, no database, no CRM, no login, so anyone can install and run them. If the GrowthNation MCP connector is also installed and you're signed in, the writing skills pull your **real customer proof** for context (via the free `prepare_*` tools) and then write the copy, falling back to web otherwise (see [Optional: the GrowthNation connector](#optional-the-growthnation-connector)).

**Using ChatGPT instead of Claude?** The skills are Claude/OpenClaw-format, but the GrowthNation MCP works in ChatGPT as an app — see [ChatGPT](#chatgpt) below.

---

## Install

### Claude Code Terminal

```bash
/plugin marketplace add growthnation/GrowthNationPlugin
/plugin install growthnation@growthnation
/reload-plugins
```

Then use `/proof-audit`, `/proof-meeting-prep`, `/proof-email`, `/proof-dm`, and `/proof-post`.

**Optional — enable auto-update:** `/plugin`, then choose `Marketplaces` tab > `growthnation` > `Enable auto-update`

### Claude Cowork / Code Desktop

1. `Customize` > `Personal Plugins` > `+` > `Create Plugin` > `Add marketplace`, input `growthnation/GrowthNationPlugin`, click `Sync`
2. `Plugins` > `Personal` > `growthnation`, click `+` on `growthnation`
3. (**Claude Cowork only**) Enable web access: `Profile` (bottom left) > `Settings` > `Capabilities` > `Code execution and file creation` > turn on `Allow network egress`, then set `Domain allowlist` to `All domains` (the skills fetch arbitrary company and LinkedIn pages).

### Claude Chat Desktop

Install from the repo URL — all five skills come with it. Use **Add marketplace**, not "Upload plugin" (a ZIP upload fails validation; the marketplace import is the supported path).

1. `Customize` > `Plugins` > `Personal` > click the `+` > **`Add marketplace`**.
2. In **URL**, paste `growthnation/GrowthNationPlugin` (or the full `https://github.com/growthnation/GrowthNationPlugin`) and click **`Sync`**. All five skills install together — you'll see "Growthnation is installed and ready to use."
3. Enable web access: `Profile` (bottom left) > `Settings` > `Capabilities` > `Code execution and file creation` > turn on `Allow network egress`, then set `Domain allowlist` to `All domains`.

### ChatGPT

ChatGPT doesn't load skills from this repo — it connects straight to the GrowthNation MCP server as a **ChatGPT app**, with Sparks and your proof library rendered as cards in the conversation:

1. In ChatGPT: `Settings` > `Apps & Connectors` > enable `Developer mode` (under Advanced settings).
2. `Create` a connector with the server URL `https://app.growthnation.ai/mcp`.
3. Sign in when prompted (OAuth) — then ask for your sparks, testimonials, or a proof-grounded email draft right in the chat.

Once the GrowthNation app is published in the ChatGPT app directory, searching "GrowthNation" in ChatGPT will replace steps 1–2.

### Other Agents (Codex / Cursor / etc.)

Copy the skill folder(s) into your agent's skills directory:

```bash
cp -r plugins/growthnation/skills/proof-audit ~/.claude/skills/          # or your agent's equivalent
cp -r plugins/growthnation/skills/proof-meeting-prep ~/.claude/skills/
cp -r plugins/growthnation/skills/proof-email ~/.claude/skills/
cp -r plugins/growthnation/skills/proof-dm ~/.claude/skills/
cp -r plugins/growthnation/skills/proof-post ~/.claude/skills/
```

Or follow your agent's skill installation instructions to install manually.

---

## Optional: the GrowthNation connector

Installing the plugin also makes the **GrowthNation MCP connector** (`https://app.growthnation.ai/mcp`) available — but the two skills never **depend** on it. They run standalone for anyone with nothing but web search + fetch.

When the connector **is** present, each skill resolves its data in steps: it checks whether the MCP is connected and you're signed in (a free `get_credits` probe), and only then reaches for the richer tools — `/proof-audit` scores against your saved proof library, `/proof-meeting-prep` grounds each person's angle in your real customer evidence, and `/proof-email`, `/proof-dm`, `/proof-post` pull your ranked customer proof + the influence angle for context (via the free `prepare_email` / `prepare_linkedin_message` / `prepare_linkedin_post` tools) and then write the copy. On any absence — not connected, not signed in, or no active trial/plan (those tools are plan-gated) — it falls back to web and still delivers. The MCP is pure upside, never a requirement.

Your agent prompts for consent before the connector runs, and the richer GrowthNation tools require a logged-in account on an active trial or plan.

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

**Proof Email**

- `/proof-email` then say who you're writing to and what you're selling.
- Or just describe it — *"write an email to the CFO at Ramp about our onboarding tool"*.

> *"Email to Dana Cole, CFO at Ramp, selling our sales-onboarding tool — we cut a peer's ramp from six weeks to nine days."* — returns a ready-to-send subject + body built on hard ROI, with the reason it works.

**Proof DM**

- `/proof-dm` then say who you're writing to and what you're selling.

> *"LinkedIn DM to a VP Sales at Notion about our proof tool."* — returns a ≤80-word DM with one sharp proof point and a frictionless ask.

**Proof Post**

- `/proof-post` then give a topic + audience.

> *"LinkedIn post on why RevOps teams miss quota, for RevOps leads at Series B SaaS."* — returns a scroll-stopping post grounded in a real customer win, ending on a question that invites comments.

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

**Proof Email / Proof DM / Proof Post** each resolve the recipient (or audience), pick the **one** influence principle that fits the role and the channel, attach the proof that carries it, and write the copy — a ready-to-send email, a ≤80-word DM, or a ≤1200-char post. With the MCP connected they pull your real ranked customer proof + the influence angle for context (free `prepare_*` tools) and then write; standalone they search the seller's site for a real proof point and research the recipient, reasoning from role × industry × stage where the web comes up empty. They never fabricate a customer, quote, or stat — no real proof means an honestly-flagged role-level claim, not an invented one.

---

## License

[MIT](LICENSE) — GrowthNation
