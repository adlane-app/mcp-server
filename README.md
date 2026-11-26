# Ad library search by Adlane

Ad library search for competitor ads: Adlane searches the public ad libraries of Meta (Facebook, Instagram), TikTok, LinkedIn and Google (Search, YouTube, Display) in one query. Look up a brand by keyword, advertiser name or website domain and see competitor ads with copy, creative, start dates, placements and landing pages. Use it as an ad spy for ad creative research and ad intelligence: save the good ones to boards and track competitors to see their new ads.

[Website](https://adlane.app) · [MCP & API docs](https://adlane.app/mcp/) · [Pricing](https://adlane.app/pricing/)

## Connect

Add `https://adlane.app/mcp` as a remote MCP server (Streamable HTTP). Your client opens Adlane, you sign in and press Allow. Works on every plan: a free account includes 5 searches to try it, no card, and you can subscribe for more. Pro API keys (`adl_…`) also work as a bearer token.

## Tools

| Tool | What it does |
| --- | --- |
| `search_ads` | Search Meta, TikTok, LinkedIn and Google by keyword, advertiser or domain. Uses one search from your plan. |
| `get_usage` | Plan, searches left and limits. |
| `list_boards` / `get_board` / `create_board` | Read and organise saved-ad boards. |
| `save_ad` | Save an ad from a search to a board, with a note. |
| `list_competitors` / `track_competitor` | Tracked brands and their new ads; start tracking one. |

## Things to ask

- "What is Gymshark running on TikTok and Meta right now? Which ads have run longest?"
- "Find LinkedIn ads for project management software and save the three best hooks to a board called Q1 ideas."
- "Track notion.so and tell me what's new since last week."

Adlane is independent of Meta, TikTok, LinkedIn and Google and shows only what their libraries publish.

## Desktop package

This npm package (`adlane-mcp`) bridges a local stdio MCP client to the hosted server at `https://adlane.app/mcp` and opens browser sign-in. Claude Desktop users can install the `.mcpb` bundle instead.

```bash
npx -y adlane-mcp
```
