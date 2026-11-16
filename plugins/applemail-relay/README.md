# InboxPip plugin

This plugin connects the inboxes you choose to your assistant through `https://inboxpip.com/mcp`. Ask for an inbox briefing, find a receipt, or prepare a reply draft. Your selected accounts and permissions control what it can do. Sending requires your approval of the final message.

The plugin contains two workflows: `inbox-briefing` and `reply-draft`. Its technical name remains `applemail-relay`; the MCP connection remains `applemailmcp` so existing identifiers stay stable. It uses the hosted service and does not include the private backend.

See the [integration kit README](../../README.md) for setup, connection controls and supported feature boundaries. This author-managed package is not an approved listing in a public marketplace. The portable manifest is provided for compatible Codex versions; OpenAI public marketplace eligibility needs clarification before submission.

## Hermes portable package

This directory also uses the portable Agent Plugins v1 format supported by current Hermes releases: `plugin.json`, a Streamable HTTP server in `mcp.json`, and two workflow skills. It contains no Python entrypoint or Desktop UI. Its stable technical name is `applemail-relay`; a catalog card may display InboxPip. Hermes catalog admission is a separate maintainer review, not implied by this repository.

## Access, cost and data disclosure

The workflow package is free and MIT licensed. It uses a separately paid InboxPip account with an active entitlement and a supported mailbox already connected by the user. The client sends MCP requests to `https://inboxpip.com/mcp`; InboxPip accesses only the mail accounts and actions in the user's grant. Mail content returned by tools is processed by the configured assistant. [Privacy](https://inboxpip.com/privacy) and [service terms](https://inboxpip.com/terms) explain the hosted service.

This package reads no local credential stores or files outside its own directory, executes no shell commands, starts no background processes, performs no self-updates and includes no telemetry. OAuth credentials are handled by the host client's supported authorization flow. The package does not contain a shared API key or require a mailbox password in chat. It adds no native tools, hooks or middleware; the host discovers available remote tools after authorization. Start with Read, and enable draft or send permissions only for workflows the user wants. Host approval controls remain in force.

For an unattended run, a missing or expired connection must stop the workflow with a connection-required message; the skill must not wait indefinitely for an interactive sign-in or look for another user's credentials. Revoke the client grant in InboxPip when disconnecting.
