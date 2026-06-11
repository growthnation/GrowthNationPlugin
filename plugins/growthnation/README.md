# GrowthNation — Proof Skills

Five self-contained social-proof skills for B2B sales, with the GrowthNation MCP connector bundled in.

| Skill | What it does |
|---|---|
| `/proof-audit` | Find a company's social proof (testimonials, case studies, reviews) and score how **fresh** it is on a five-band scale, then recommend what to refresh. |
| `/proof-meeting-prep` | Read every person in a sales call — role priorities, likely objections — and hand back the one proof angle that lands for each, plus how to sequence the room. |
| `/proof-email` | Write a ready-to-send cold/warm sales email (subject + body) grounded in real proof and one influence principle, tailored to the recipient's role. |
| `/proof-dm` | Write a short LinkedIn DM (≤80 words) that earns a reply — one sharp proof point, one frictionless ask. |
| `/proof-post` | Write a public LinkedIn post that pulls inbound, tuned to a target audience. |

## Install

```bash
openclaw plugins install clawhub:@growthnation/plugin
```

## Standalone by default

Every skill runs on the agent's built-in **web search + fetch** — no API keys, no database, no login. Anyone can install and run them.

## Optional: the GrowthNation connector

The bundled MCP connector (`https://app.growthnation.ai/mcp`, OAuth) is optional. When it's connected and you're signed in, the writing skills ground in **your real GrowthNation customer proof** via the free `prepare_*` tools, then write the copy — falling back to web search otherwise.

Learn more: https://growthnation.ai/agents
