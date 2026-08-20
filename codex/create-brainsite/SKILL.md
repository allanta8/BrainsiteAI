---
name: create-brainsite
description: Create an unclaimed BrainSite AI-agent preview for a person or business from their X (Twitter) profile handle, display name, and bio, via BrainSite's remote MCP server. Use when Allan asks to create a BrainSite for someone, generate a BrainSite listing from an X profile, or test the create_brainsite_from_x_profile tool.
---

# Create BrainSite from an X Profile

Creates an unclaimed BrainSite AI-agent preview from a person or business's X profile: handle, display name, and bio. Returns a live preview URL and a claim link the person can use to take ownership. One-way create operation only — never posts, replies, DMs, or takes any action on X itself.

## Connect the MCP server (once per environment)

Add BrainSite's remote MCP server to Codex's MCP config (`~/.codex/config.toml`, `mcp_servers` section) if it isn't already there:

```toml
[mcp_servers.brainsite]
url = "https://www.brainsite.ai/api/v1/mcp"
transport = "http"
headers = { Authorization = "Bearer <BRAINSITE_MCP_SECRET>" }
```

Get `<BRAINSITE_MCP_SECRET>` from Allan directly. Never hardcode it in this file, commit it, or paste it into chat. Confirm the exact config key names against the installed Codex CLI's own MCP documentation before relying on this — the shape above is a best-effort template, not a verified command. Once connected, `create_brainsite_from_x_profile` is available as a normal tool.

## Using the tool

Call `create_brainsite_from_x_profile` with:

- `x_handle` (required) — the X handle, no `@`.
- `display_name` (required) — the person or business's name.
- `bio` (optional, recommended) — a short bio; produces a noticeably better preview.
- `tweet_url` (optional) — the post that prompted this, if there was one.
- `requested_by_handle` (optional) — who requested it, if different from the target.

## Guardrails

- Only call this with a specific named person/handle Allan actually wants listed. Don't create previews speculatively or in a batch without being asked.
- If the tool returns a "preview already exists" error, report that and stop — don't retry with variations to force a new one.
- After creating a preview, hand Allan the preview and claim links. Never post, DM, or reply anywhere on the target's behalf — creating the preview is the only action this tool is for.
- Note that BrainSite previews are marked "unofficial, not affiliated until claimed" and the actual person can claim or request removal of it.
