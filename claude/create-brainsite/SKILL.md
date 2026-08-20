---
name: create-brainsite
description: Create an unclaimed BrainSite AI-agent preview for a person or business from their X (Twitter) profile handle, display name, and bio, via BrainSite's remote MCP server. Use when Allan or a user asks to create a BrainSite for someone, generate a BrainSite listing from an X profile, or test the create_brainsite_from_x_profile tool.
---

# Create BrainSite from an X Profile

Creates an unclaimed BrainSite AI-agent preview from a person or business's X profile — handle, display name, and bio. Returns a live preview URL and a claim link the person can use to take ownership. This is a one-way create operation: it never posts, replies, DMs, or takes any action on X itself.

## Connect the MCP server (once per environment)

If BrainSite's MCP server isn't already connected:

```
claude mcp add --transport http brainsite https://www.brainsite.ai/api/v1/mcp --header "Authorization: Bearer <BRAINSITE_MCP_SECRET>"
```

Get `<BRAINSITE_MCP_SECRET>` from Allan directly. Never hardcode it in this file, commit it, or paste it into chat. Once connected, `create_brainsite_from_x_profile` is available as a normal tool.

## Using the tool

Call `create_brainsite_from_x_profile` with:

- `x_handle` (required) — the X handle, no `@`.
- `display_name` (required) — the person or business's name.
- `bio` (optional, recommended) — a short bio; produces a noticeably better preview.
- `tweet_url` (optional) — the post that prompted this, if there was one.
- `requested_by_handle` (optional) — who requested it, if different from the target.

## Guardrails

- Only call this with a specific named person/handle the user actually wants listed. Don't create previews speculatively or in a batch without being asked.
- If the tool returns a "preview already exists" error, report that and stop — don't retry with variations to force a new one.
- After creating a preview, hand the user the preview and claim links. Never post, DM, or reply anywhere on the target's behalf — creating the preview is the only action this tool is for.
- Note in your response that BrainSite previews are marked "unofficial, not affiliated until claimed" and the actual person can claim or request removal of it.
