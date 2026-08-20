---
name: Reply with a BrainSite
category: Marketing
added_at: "2026-08-19T00:00:00.000Z"
contributor: @BrainsiteAI
integrations: [BrainSite]
---

Set up a new bot for me I can trigger whenever I want to create a BrainSite listing, in its own dedicated chat. Connect to BrainSite's MCP server at https://www.brainsite.ai/api/v1/mcp, with the shared secret set as a Bearer token in the Authorization header, never pasted into chat. Then configure it: ask me for the X profile to use, mine by default or another handle I name, read that profile's handle, display name, and bio, then call the create_brainsite_from_x_profile tool with that handle, name, and bio. Never post, reply, or take any action on X itself, just create the preview and show me the preview and claim links. Do a dry run on one profile I name so I can check the output before it goes live, then save it.
