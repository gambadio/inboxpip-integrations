# InboxPip — connect your email to your AI

Connection files and two useful email workflows for the hosted [InboxPip service](https://inboxpip.com). The website and OAuth discovery endpoint are live. This package is maintained by InboxPip; it is not an approval or listing in Anthropic's or OpenAI's public marketplace. Individual client and provider qualification remains separate.

Ask your assistant to find a receipt, summarize unread mail, or draft a reply. InboxPip connects the email accounts you choose and restricts each assistant to the accounts and permissions you approve.

## Start here

1. **Connect an inbox.** Open InboxPip, create your account, then choose **Add email account** in your dashboard. Choose your email provider and follow its on-screen instructions. An email provider may require an app password or administrator permission. Never paste your password into an AI chat.
2. **Connect your AI.** Open the [connection guide](https://inboxpip.com/connect), choose your client, and use `https://inboxpip.com/mcp`. Sign in to InboxPip when its authorization page opens. Select only the inboxes and permissions you want this assistant to use; start with Read.
3. **Try one useful task.** Say: “Show which inboxes you can access, then summarize unread mail from my work inbox without changing anything.” If you add another inbox later, reconnect the assistant and approve that inbox explicitly.

This connector requires an InboxPip account and an active plan or eligible promotional access. AI-client availability depends on the client's plan, terms and administrator settings.

## Claude Code

For a direct MCP connection:

```sh
claude mcp add --transport http applemailmcp https://inboxpip.com/mcp
```

Open Claude Code, run `/mcp`, choose the InboxPip connection and complete authorization. The server may be shown under its stable technical name `applemailmcp`.

To install the two workflow skills and the bundled connection from this repository:

```sh
claude plugin marketplace add gambadio/inboxpip-integrations
claude plugin install applemail-relay@inboxpip
```

Use either the direct connection or the plugin's bundled connection to avoid duplicate tools. The marketplace above is our own integration package, not Anthropic's public directory. To validate a local checkout, use `claude plugin validate --strict .` and `claude plugin validate --strict plugins/applemail-relay`.

## Codex

Connect through the Codex MCP settings or run:

```sh
codex mcp add applemailmcp --url https://inboxpip.com/mcp
codex mcp login applemailmcp
```

Select the inboxes and permissions in the browser consent screen. If your Codex version supports plugins, install the workflow package with:

```sh
codex plugin marketplace add gambadio/inboxpip-integrations
codex plugin add applemail-relay@inboxpip
```

Restart the client if newly installed skills do not appear. Do not install a second copy of the same MCP connection. These commands install an author-managed package; they do not submit it to the OpenAI marketplace. Public OpenAI marketplace submission is on hold because the current rules restrict unofficial third-party connector and pass-through plugins.

## Other clients

The hosted endpoint uses Streamable HTTP and OAuth with dynamic client registration. Clients that support and permit that combination can be evaluated using the connection guide. If the client supports only bearer authentication, generate a revocable API key scoped to the intended inboxes and permissions in InboxPip; keep it in the client's credential store, never in a shared file or prompt.

Claude web custom connectors, ChatGPT custom connections and agent frameworks require separate live checks under the relevant plan and administrator settings. Grok and Cursor commercial access is not assumed. “Muse” has not been identified or verified. We do not advertise these as tested integrations.

## Features and limits

- Fourteen mail tools: discover granted accounts, list folders, search/read mail and attachments, save drafts, send approved messages, move/copy/flag messages, and manage custom folders. Exact availability depends on the current account and token permissions.
- Multiple explicit inbox grants. Use `list_mail_accounts` first and pass its returned `accountId` with mail operations. Revoking, replacing or downgrading an inbox does not grant access to another one.
- iCloud Calendar with separate permissions. Calendar is available; invitations and recurring-event changes are not supported.
- Reminders and Notes remain beta and require the optional awake Mac companion. Notes supports plain-text reading and new notes, not editing existing notes or exporting locked notes and attachments.

The implementation has 15 IMAP/SMTP setup presets; a preset is guidance, not proof every provider/account has passed a live test. SMTP sends mail; reading requires IMAP or a supported provider API. Google and Microsoft OAuth code is implemented, but the production provider applications still need registration and verification. Proton-style local bridges and private-network-only mail servers do not become accessible to this cloud service merely by entering an address.

## Your controls

Read-only is a useful starting point. Grant Drafts, Send, Organize, Folders or Delete only when needed. InboxPip and your chosen AI service process requested mail contents; do not interpret encrypted stored credentials as end-to-end encryption of mailbox content. Review the [privacy notice](https://inboxpip.com/privacy) and [terms](https://inboxpip.com/terms). Disconnect or revoke a client from your InboxPip dashboard when you no longer want it to have access.

InboxPip is operated independently by Datenkraft Kupper. It is not affiliated with or endorsed by Apple, Google, Microsoft, Anthropic or OpenAI. Provider names describe connection options.

## Package layout and license

`plugins/applemail-relay/plugin.json` and `mcp.json` use the portable Agent Plugins format. `.claude-plugin/plugin.json` and `.mcp.json` provide Claude's format. Both use the same two `skills/` directories. No secrets, private mailbox contents or backend code are included. The MIT license covers only this integration kit; the hosted service has separate terms. For security issues, follow [SECURITY.md](SECURITY.md).

Current technical sources: [Claude MCP setup](https://code.claude.com/docs/en/mcp), [Claude plugin publishing](https://code.claude.com/docs/en/plugins/publish), [OpenAI plugin packaging](https://developers.openai.com/plugins/build/plugins), [OpenAI plugin guidelines](https://developers.openai.com/plugins/plugin-guidelines).
