# Adlane MCP

An advertising workspace for Google and Meta campaign planning and review.

get_profile reads your own account. list_workspaces lists your own advertising workspaces. Neither tool creates campaigns, approves proposals, changes ads or budgets, or spends money.

## Remote MCP

Use **https://mcp.adlane.app/mcp** in a client that supports remote MCP with OAuth. Sign in to Adlane and explicitly approve the connection.

## Claude Desktop and other stdio clients

Requires Node.js 22 or newer. Add this configuration:

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

Or install the `.mcpb` file from [Releases](https://github.com/adlane-app/mcp-server/releases) in your desktop client's Extensions settings. The connector opens your browser for sign-in. If the consent page asks you to sign in, use its new-tab link, then return and refresh the consent page.

## Privacy and permissions

Your product password and provider credentials are not requested by this package. The pinned [mcp-remote](https://www.npmjs.com/package/mcp-remote) bridge handles OAuth, PKCE and local token storage. It connects only to the fixed endpoint above; command-line endpoint overrides are not supported. OAuth tokens are stored locally by mcp-remote and should be treated as credentials.

Revoke a connection at [Adlane MCP connections](https://adlane.app/oauth/mcp/connections).

## Development and publishing

Run `npm ci` and `npm test`. GitHub Actions publishes a new package version using the organization’s `NPM_TOKEN` secret, then builds and releases the desktop bundle. Keep package.json, manifest.json, server/config.json and server.json versions aligned.

Marketplace approval is separate from npm publication. See the product’s submission notes for endpoint tests and review prerequisites.

[Website](https://adlane.app) · [Issues](https://github.com/adlane-app/mcp-server/issues)
