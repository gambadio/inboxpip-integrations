# InboxPip plugin

This plugin connects the inboxes you choose to your assistant through `https://inboxpip.com/mcp`. Ask for an inbox briefing, find a receipt, or prepare a reply draft. Your selected accounts and permissions control what it can do. Sending requires your approval of the final message.

The plugin contains two workflows: `inbox-briefing` and `reply-draft`. Its technical name remains `applemail-relay`; the MCP connection remains `applemailmcp` so existing identifiers stay stable. It uses the hosted service and does not include the private backend.

See the [integration kit README](../../README.md) for setup, connection controls and supported feature boundaries. This author-managed package is not an approved listing in a public marketplace. The portable manifest is provided for compatible Codex versions; OpenAI public marketplace eligibility needs clarification before submission.
