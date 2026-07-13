![GrowthNation](assets/logo.svg)
[![SPONSORED BY E2B FOR STARTUPS](https://img.shields.io/badge/SPONSORED%20BY-E2B%20FOR%20STARTUPS-ff8800?style=for-the-badge)](https://e2b.dev/startups)

# GrowthNation — MCP connector for AI agents

One plugin, one connector, no bundled skills: plug any agent into your company's
**Agentic Transformation OS**.

GrowthNation interviews your whole team by voice, turns what they actually do into
per-department **AI agent skills** (security-audited, quality-scored, versioned), and
serves them — together with your company's connected tools — through a single MCP
server. This plugin is the door: `https://app.growthnation.ai/mcp`, OAuth, no API keys.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

---

## What your agent gets after signing in

| Surface | What it is |
|---|---|
| **Your skill library** | One tool per skill your departments own — generated from voice interviews with your team, served fork-first (your personal version when you have one, the team's otherwise). Calling a skill returns its full bundle for the agent to run. |
| **Your connected tools** | Google Workspace (Calendar, Drive, Sheets, Docs, Slides, Forms, Ads, Gmail), Slack, Notion, GitHub, Asana, Apollo, Fireflies, Fathom, Granola and more — one router tool per connector, credentials held server-side by your company. |
| **`start-interview`** | Kick off your own voice interview — it feeds your department's skill library. |
| **`department-audit`** | Your interview-grounded AI-readiness scorecard (the real one, not public-signal guesswork). |
| **`create-skill`** | Propose a new skill into the company library — a manager approves, everyone gets it. |
| **`report-feedback`** | Tell it when a skill or tool misbehaves — your personal skill version regenerates within ~2 minutes; check back for the new version. |

---

## Install

### Claude Code Terminal

```bash
/plugin marketplace add growthnation/GrowthNationPlugin
/plugin install growthnation@growthnation
/reload-plugins
```

Then sign in when the `growthnation` connector prompts (OAuth).

**Optional — enable auto-update:** `/plugin`, then choose `Marketplaces` tab > `growthnation` > `Enable auto-update`

### Claude Cowork / Code Desktop

1. `Customize` > `Personal Plugins` > `+` > `Create Plugin` > `Add marketplace`, input `growthnation/GrowthNationPlugin`, click `Sync`
2. `Plugins` > `Personal` > `growthnation`, click `+` on `growthnation`
3. Approve the `growthnation` connector when prompted and sign in (OAuth).

### Claude Chat Desktop

Use **Add marketplace**, not "Upload plugin" (a ZIP upload fails validation; the marketplace import is the supported path).

1. `Customize` > `Plugins` > `Personal` > click the `+` > **`Add marketplace`**.
2. In **URL**, paste `growthnation/GrowthNationPlugin` (or the full `https://github.com/growthnation/GrowthNationPlugin`) and click **`Sync`** — "Growthnation is installed and ready to use."
3. Open the plugin's **Connectors** tab and sign in to `growthnation` (OAuth).

### ChatGPT

ChatGPT connects straight to the same MCP server as a **ChatGPT app**:

1. In ChatGPT: `Settings` > `Apps & Connectors` > enable `Developer mode` (under Advanced settings).
2. `Create` a connector with the server URL `https://app.growthnation.ai/mcp`.
3. Sign in when prompted (OAuth) — your skills and tools appear in the conversation.

### Other Agents (Codex / Cursor / etc.)

Add the MCP server to your agent's MCP configuration:

```json
{
  "mcpServers": {
    "growthnation": {
      "type": "http",
      "url": "https://app.growthnation.ai/mcp"
    }
  }
}
```

---

## Usage

Once connected, just work — the agent reaches for your skills when a task matches
(each skill's description tells it when), and for your connected tools when it needs
your systems. Useful direct asks:

- *"What skills do I have?"* — lists your library.
- *"Run my department audit."* — your AI-readiness scorecard.
- *"Start my interview."* — feed the library with what you actually do.
- *"That deck skill produced 40 pages — report it."* — feedback regenerates your
  version within ~2 minutes.

## How it works

Your company runs GrowthNation: the org chart maps departments, an AI agent interviews
every employee by voice, and per-department skills are generated from the transcripts —
then security-audited, quality-scored, and versioned. Employees' feedback refines their
own fork of a skill; managers approve the best forks into the team version. This MCP is
the single serving surface for all of it, plus the gateway to your company's connected
SaaS tools. Your IP stays with the company; credentials stay server-side.

Learn more: https://growthnation.ai

## License

MIT — see [LICENSE](LICENSE).
