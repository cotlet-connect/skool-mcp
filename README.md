# Skool API integration and MCP server: connect Skool to ChatGPT, Claude and any AI agent

Skool API integration and MCP server, unofficial, by Cotlet. Your AI works in your own signed-in Skool account: members, membership questions, courses, pending requests, revenue and affiliates, on the same screens your login opens. Cotlet has 71 ready Skool tools for AI agents, and the Cloud Browser does the rest. No developer and no Skool API key needed. Cotlet is independent and is not affiliated with Skool.

**Does Skool have an API or an MCP server?** Skool has no public API and no webhooks (checked 22 Nov 2026). Its Zapier app needs the Pro plan and has two triggers, answered membership questions and new paid member, and two actions, invite member and unlock course; Make has one module. Skool has no MCP server and no ChatGPT or Claude app.

## What Skool community owners ask their AI to do in Skool

| Job | Ask your AI | Make it repeat |
|---|---|---|
| Member list | "Export my member list with tier, join date and email to a spreadsheet." | Weekly |
| Membership-question answers | "Copy yesterday's membership-question answers into my sheet with name and email." | Every morning |
| New paid members to your CRM | "List this week's new paid members with their answers, ready for GoHighLevel or Kit." | Daily, through your own endpoint |
| Members going quiet | "Which members have not been active for 30 days? Sort them by tier." | Weekly |
| Cancelled members | "List members whose paid membership ended this week, so I can remove them from my app." | Daily |
| Course access | "Unlock the Pro course for the buyers in this list. Show me before you change anything." | When a sale comes in elsewhere |
| Pending requests | "List pending membership requests and flag the ones that look like spam. Approve nothing yet." | Daily |
| Revenue and affiliates | "Show this month's revenue, new paid members, cancellations and affiliate payouts." | Monthly |
| Answers from your classroom | "Find the lesson in my classroom that answers this member's question." | When a member asks |
| Post drafts | "Draft next week's three community posts from my notes. I will post them myself." | Weekly |
| Leaving Skool | "Download my member list and my course outlines before I move." | Once |

Your AI asks you before it changes anything. It drafts posts and messages for you to send yourself: Skool's platform policy asks owners not to use bots to post, comment or message others. Payments stay in your hands: Cotlet refuses payments.

## Your own Skool API, built with Cotlet

Skool gives you no public API, only a group key for its Zapier plugin on the Pro plan. With Cotlet you build your own: your AI does the job once in your Cloud Browser, you save it as an endpoint, and you call it from Google Sheets, Airtable, GoHighLevel, Kit, Mailchimp, n8n, Make, Zapier, your own app.

Examples you can build in a few minutes (none of them exists until you build it):

| Endpoint you build | What it returns or does |
|---|---|
| `members-export` | name, email, tier, join date and status of each member |
| `new-paid-members` | paid members since a date, with their membership-question answers |
| `membership-answers` | answers to membership questions since a date |
| `inactive-members` | members with no activity for a number of days |
| `cancelled-members` | members whose paid membership ended in a period |
| `pending-requests` | membership requests waiting for approval |
| `revenue-summary` | revenue, new paid members, cancellations and affiliate payouts for a period |
| `unlock-course` | unlocks a course for a member (writes only after you allow it) |
| `invite-member` | invites a member by email (writes only after you allow it) |

Call it with your Cotlet API key, JSON in and JSON out:

```bash
curl -X POST https://cotlet.dev/api/v1/custom/members-export \
  -H "Authorization: Bearer $COTLET_API_KEY" -H "Content-Type: application/json" -d '{}'
```

Limits: one call runs up to 90 seconds, writes wait for your consent, payments are blocked. Start here: https://cotlet.dev/app/custom-api/new?app=skool

## Connect in 2 minutes

Sign up at https://cotlet.dev, sign in to Skool once in your Cloud Browser, then add Cotlet to your AI.

### Claude

Settings → Connectors → Add custom connector, paste `https://cotlet.dev/mcp/v1` and sign in with Cotlet.dev.

### ChatGPT

Open Plugins in ChatGPT, choose Create as a plugin, paste `https://cotlet.dev/mcp/v1` and sign in with Cotlet.dev. No API key needed.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Questions from Skool community owners
**How do I connect Skool to GoHighLevel, Kit or Mailchimp?**

Build a `new-paid-members` endpoint once and call it from GoHighLevel, Kit, Mailchimp, Zapier, Make or n8n, with the tier and the membership-question answers as tags.

**How do I connect Skool to Make or n8n beyond inviting a member?**

Skool's Make app has one module. With Cotlet you build your own Skool endpoints, such as `members-export` or `cancelled-members`, and call them from Make or n8n.

**How do I keep a live Skool member list in Google Sheets or Airtable?**

Call your `members-export` endpoint from Google Sheets or Airtable on a schedule, or ask your AI to download the list each week.

**How do I remove access in my own app when a Skool membership ends?**

Skool's Zapier app has no trigger for ended memberships. A `cancelled-members` endpoint lists them every day, and your app or n8n removes their access.

**How do I give buyers from ThriveCart, Stripe or Square their Skool course?**

Call your own `unlock-course` endpoint when the sale comes in. It writes only after you allow writes for it.

**How do I export my Skool member list with emails?**

Your AI downloads the member list your owner login can see, with tier and join date, as a spreadsheet.

**Can AI reply to comments or send DMs in Skool for me?**

Read Skool's platform policy first: it asks owners not to use bots to post, comment or message others, and not to scrape data or make automation requests. Use your AI to draft replies and posts that you send yourself.

**Can AI tell me which Skool members are likely to cancel?**

It lists members who went quiet, sorted by tier and join date, so you can reach out yourself before they leave.

**Is Cotlet affiliated with Skool?**

No. Cotlet is independent and not affiliated with Skool.

## Find it on

- [Skool MCP server on Cotlet.dev](https://cotlet.dev/integrations/skool-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=skool&utm_content=find)
- [PyPI package skool-mcp](https://pypi.org/project/skool-mcp/)

## More community and course apps on Cotlet

- [Substack MCP](https://github.com/cotlet-connect/substack-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Patreon MCP](https://github.com/cotlet-connect/patreon-mcp)
