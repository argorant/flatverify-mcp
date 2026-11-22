# Flatverify MCP server

Verify email addresses from ChatGPT, Claude, Cursor or any MCP client, on a flat monthly plan. Every plan is
unlimited; plans differ only in speed.

Flatverify by Argorant checks whether an address can receive mail. Each address comes back **valid**, **invalid**,
**risky** or **unknown**, with a one-word reason (`catch_all`, `role_account`, `disposable`, `mailbox_not_found` and
more) and the flags disposable, role, free and catch_all.

- Endpoint: `https://mcp.flatverify.com/mcp` (streamable HTTP)
- Sign-in: OAuth 2.1 with dynamic client registration, or a Flatverify API key as `Authorization: Bearer fv_...`
- Website: https://flatverify.com
- Docs: https://flatverify.com/docs

## Connect

**Claude**: Settings, Connectors, Add custom connector, URL `https://mcp.flatverify.com/mcp`, then sign in to
Flatverify and approve.

**ChatGPT**: Settings, Apps and Connectors, Advanced, Developer mode, Create, URL `https://mcp.flatverify.com/mcp`.

**Cursor, Windsurf, VS Code and other clients** (`mcp.json`):

```json
{
  "mcpServers": {
    "flatverify": {
      "url": "https://mcp.flatverify.com/mcp"
    }
  }
}
```

**With an API key** (scripts, agents, clients without OAuth): create a key in the Flatverify app under API keys and
send it as a header.

```json
{
  "mcpServers": {
    "flatverify": {
      "url": "https://mcp.flatverify.com/mcp",
      "headers": { "Authorization": "Bearer fv_your_key" }
    }
  }
}
```

## Tools

| Tool | What it does | Read only |
| --- | --- | --- |
| `verify_email` | Checks one address and answers at once | no |
| `start_bulk` | Starts a list as a background job (up to 10,000 per call) | no |
| `get_job` | Job status and counts, plus paged per-address results | yes |
| `get_usage` | Your plan and speed | yes |
| `health` | Whether Flatverify is up | yes |
| `search` | Help articles and jobs by id | yes |
| `fetch` | Full help article or job summary by id | yes |

No tool deletes anything, and no tool spends money: every plan is flat.

## Things to ask

- "Verify maya.chen@amazon.com."
- "Here are 40 signups from this week. Which ones should I drop?"
- "Check every address in this CSV and give me only the valid ones."
- "Start a job for this list, tell me when it is done, then show me the risky rows with their reason."
- "Which of these are role addresses like info@ or sales@?"

## Use cases

- **Clean a list in chat.** Paste addresses or attach a file and say "verify these". The assistant tells you which
  rows to drop.
- **Check before you send.** Before a campaign, ask your assistant to verify the list and remove the invalid rows.
- **Gate a signup flow you are building.** In Cursor, let the agent call `verify_email` while it writes and tests
  your signup code.
- **Route by reason.** Ask for catch-all and role addresses separately, so they go to a softer step instead of
  straight out.

## Plans

Every plan is unlimited. Plans differ only in how many addresses per minute you can check. Details on
https://flatverify.com/pricing.

## Privacy and terms

- Privacy: https://flatverify.com/privacy
- Terms: https://flatverify.com/terms

Operated by Argorant. Questions: dev@argorant.com.
