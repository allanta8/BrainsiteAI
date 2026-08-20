# BrainsiteAI

Agent skills for creating a [BrainSite](https://www.brainsite.ai) AI-agent preview directly from an X (Twitter) profile — handle, display name, and bio in, a live preview and claim link out. No signup required to see the result.

All three skills call the same public capability: BrainSite's remote MCP server at `https://www.brainsite.ai/api/v1/mcp`, exposing one tool, `create_brainsite_from_x_profile`. Fixing or extending that one endpoint updates all three at once.

## Skills

| Platform | Path | Notes |
|---|---|---|
| Claude | [`claude/create-brainsite/SKILL.md`](claude/create-brainsite/SKILL.md) | Drop into `.claude/skills/create-brainsite/` in any Claude Code project, or add as a Claude.ai custom skill. |
| Codex | [`codex/create-brainsite/SKILL.md`](codex/create-brainsite/SKILL.md) | Drop into `~/.codex/skills/create-brainsite/`. |
| Grok Bot | [`grok/create-brainsite.md`](grok/create-brainsite.md) | Submission format for [botdirectory.ai](https://botdirectory.ai) — matches its `bots/*.md` convention (YAML frontmatter + a natural-language setup prompt). |

## Connecting

Every skill needs the same two things:

1. **MCP server URL:** `https://www.brainsite.ai/api/v1/mcp`
2. **Auth:** a shared secret, sent as a standard `Authorization: Bearer <secret>` header. Get the secret from Allan directly — it is intentionally not committed anywhere in this repo.

## Tool reference

**`create_brainsite_from_x_profile`**

| Field | Required | Description |
|---|---|---|
| `x_handle` | yes | X handle, no `@`. |
| `display_name` | yes | The person or business's name. |
| `bio` | no | Short bio; produces a better preview. |
| `tweet_url` | no | URL of a post that prompted this, if any. |
| `requested_by_handle` | no | Who requested it, if different from the target. |

Returns `{ demo_token, preview_url, claim_url }`. Never posts, replies, DMs, or takes any action on X — creating the preview is the only side effect.
