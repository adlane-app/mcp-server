# Adlane MCP

**A clearer next move in Google and Meta advertising.**

Adlane is an AI workspace for paid marketing. Bring your business website, goal and target market, connect Google or Meta ad accounts, and explore the evidence behind campaign decisions in one conversation. The product brings campaign analysis, market research and proposals together so teams can review the exact action before changing a live account.

[Website](https://adlane.app) · [MCP repository](https://github.com/adlane-app/mcp-server) · [Agent skill](https://github.com/adlane-app/agent-skill) · [npm package](https://www.npmjs.com/package/adlane-mcp)

## What this connector does

This package connects a local stdio MCP client to the hosted [Adlane MCP server](https://mcp.adlane.app/mcp). Hosted tools run on Cloudflare; the local package bridges the connection and opens browser-based OAuth. You do not need to deploy a Worker or paste a product password into your assistant.

| Tool | What it does |
| --- | --- |
| `get_profile` | Read the signed-in account context. |
| `list_workspaces` | List advertising workspaces owned by the account. |
| `list_ad_accounts` | Find owned, connected advertising accounts. |
| `get_campaign_performance` | Read campaign reporting for the selected account and reporting window. |
| `get_campaign_details` | Inspect campaign configuration and status before interpreting results. |

The MCP is read-only: it cannot create campaigns, approve proposals, change ads or budgets, or spend money. Campaign creation and approved live changes belong to the Adlane application. Preserve each platform’s attribution context; conversion value is not profit and overlapping conversions are not unique customers.

## Example workflow

1. Choose the owned workspace and ad account; note the reporting currency and timezone.
2. Compare equal-length date ranges and inspect campaign details where a change needs explanation.
3. Return observed changes and proposed next steps for review in Adlane, without modifying the account.

### Things to ask your assistant

> Compare the last two complete weeks for my selected ad account. Show spend and conversion changes with the reporting currency.

> Which campaigns need a closer look? Read their current status before suggesting next steps.

> Prepare a short review of Google and Meta performance without treating cross-platform conversions as unique sales.

## Connect a remote MCP client

1. Open the client’s custom MCP or connector settings.
2. Enter `https://mcp.adlane.app/mcp` as the remote server URL.
3. Complete Adlane sign-in in your browser and review the permissions on the consent screen.
4. Return to the client and load the available tools.

Use a client that supports Streamable HTTP MCP and OAuth. Custom-connector availability depends on the client and your account. A public repository or npm release does not mean the integration has been approved for a client’s marketplace.

## Claude Desktop and other stdio clients

Requires **Node.js 22 or newer** and an existing Adlane account. Add this entry to your client’s MCP configuration:

```json
{
  "mcpServers": {
    "adlane": {
      "command": "npx",
      "args": [
        "-y",
        "adlane-mcp"
      ]
    }
  }
}
```

You can also run `npx -y adlane-mcp` from a terminal to start the bridge. It speaks MCP over stdio; it is not an interactive chat interface. For desktop clients that support MCPB extensions, download the `.mcpb` file from [Adlane releases](https://github.com/adlane-app/mcp-server/releases).

## Permissions and account access

Requested scopes: `profile:read ads:read`. Older profile-only connections need to reconnect and explicitly approve the additional permissions before content tools are available.

Only approve a connection you intended to start. If sign-in opens a new tab, finish it, return to the consent screen and refresh. [Manage or revoke connected apps](https://adlane.app/oauth/mcp/connections).

The package uses pinned [`mcp-remote`](https://www.npmjs.com/package/mcp-remote) for OAuth, PKCE and local token storage. Tokens on your computer are credentials. The connector uses the fixed endpoint above and rejects command-line endpoint overrides. Product passwords and underlying provider credentials are not requested by this package.

## Troubleshooting

- **No tools or insufficient permissions:** reconnect through browser consent and check the selected account.
- **An empty list:** confirm that the account owns the expected items. Empty results are different from a failed request.
- **A link asks you to sign in:** open it with the owning product account; a private product link is not a public share link.
- **The browser blocks authorization:** inspect the browser’s displayed error and restart an expired request from the client. Never send cookies or tokens in an issue.

## Add the companion skill

The [Adlane agent skill](https://github.com/adlane-app/agent-skill) explains how to select the right records, interpret results and respect the workflow’s limits:

```sh
npx skills add adlane-app/agent-skill
```

## Learn more about Adlane

- [Paid-marketing workspace](https://adlane.app/)
- [Product capabilities](https://adlane.app/#product)
- [Getting started](https://adlane.app/#how-it-works)
- [Common questions](https://adlane.app/#questions)
- [Open Adlane](https://adlane.app/app/)
- [Privacy](https://adlane.app/privacy/)

## Development and support

```sh
npm ci
npm test
npm run bundle
```

[Report a connector issue](https://github.com/adlane-app/mcp-server/issues) with your client, Node.js version and a redacted error. Keep `package.json`, `manifest.json`, `server/config.json`, `server.json` and the lockfile version aligned for releases. GitHub Actions publishes versioned npm packages and MCPB assets. See [LICENSE](https://github.com/adlane-app/mcp-server/blob/main/LICENSE) for the MIT license.
