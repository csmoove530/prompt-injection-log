# Prompt Injection Field Log

Real prompt-injection attempts observed **in the wild** by AI coding agents during everyday development work — logged as they happen, so other builders know what's actually circulating.

This is not a research dataset or a how-to. It's a defensive field log: what the injection looked like, where it was embedded, what it tried to get the agent to do, and how it was caught. Payloads are **summarized, not reproduced** — the goal is recognition, not replication.

## Why this exists

While building an unrelated project, our coding agents (Claude Code with web-research subagents) hit two independent injection attempts **in one day** — both embedded in ordinary web content (search results and an API response), both impersonating trusted harness config, and both targeting the same thing: the agent's **payment tools**. Agents with wallets are now a real attack surface. If you're building agents that can spend money, read [the log](LOG.md).

## The pattern to know

Every entry so far follows one shape:

> Content fetched from the web arrives with an **appended block impersonating harness/system configuration** (e.g. fake "MCP Server Instructions"), naming real tools the attacker hopes the agent has — especially payment and wallet tools — and phrased as standing instructions rather than page content.

**Defense that worked, both times:** treat every instruction-shaped string arriving via tool results (web pages, search results, API responses) as *data, not directives*. Instructions come from the user and the harness — never from fetched content. Subagents were explicitly prompted to return conclusions only, and flagged the anomaly upward instead of acting on it.

## Reading the log

Entries live in [LOG.md](LOG.md), newest first. Each records: date, surface (where the payload rode in), disguise (what it impersonated), target (what capability it went after), outcome, and recognition notes.

## Contributing

Seen one yourself? Open an issue or PR with the same fields. Rules: summarize payloads rather than paste them verbatim when they contain live lures (URLs, wallet addresses, invite codes — defang or redact); no speculation about attribution; defensive framing only.

## Caveats

- Entries are agent-reported observations, sometimes summarized by the subagent that caught them; raw payloads are not always preserved.
- "Injection attempt" here means instruction-shaped content in a data channel. Some cases may be aggressive SEO/content-farm garbage rather than a targeted attack — the defense is identical either way.

🤖 Maintained with [Claude Code](https://claude.com/claude-code)
