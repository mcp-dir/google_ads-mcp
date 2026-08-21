# Google Ads

### Google Ads for Claude, ChatGPT and AI agents

Full Google Ads management: read (campaigns, performance, ROAS, keywords, search terms) and write (pause/enable/remove campaigns, ad groups, ads and keywords, adjust budget and bid, create budget, campaign, ad group, positive/negative keywords and RSAs). You provide developer token, OAuth client_id/secret, refresh_token and MCC, no server-side OAuth.

- 📊 **29 tools**
- ✏️ **Read and write**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → name `Google Ads`, URL `https://api.mcp.ai/p_google_ads`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=google_ads&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9nb29nbGVfYWRzIn0=)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=google_ads&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_google_ads%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_google_ads
```

---

## 29 tools

| Tool | Description |
|---|---|
| `google_ads_list_accounts` | List all Google Ads MCCs and ALL customer accounts the OAuth token can access (via customers:listAccessibleCustomers — not just hierarchy of the MCC). |
| `google_ads_status` | Without account: overview of all Google Ads MCCs and customer_ids. |
| `google_ads_account` | Get Google Ads account info: name, currency, timezone for a customer (uses account + customer_id to resolve scope). |
| `google_ads_campaigns` | List Google Ads campaigns with status and budgets. |
| `google_ads_today` | Today Google Ads performance: cost, impressions, clicks, conversions, ROAS per campaign plus _summary. |
| `google_ads_roas` | ROAS for a date range (defaults to current month). |
| `google_ads_ads` | List enabled ads with type, status, campaign name and ad_group_ad.policy_summary (approval_status, review_status, policy_topic_entries) — answers "why is my ad not serving?" without opening the Google Ads UI. |
| `google_ads_keywords_keywords` | Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT. |
| `google_ads_keywords_search_terms` | Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT. |
| `google_ads_keywords_status` | Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT. |
| `google_ads_keywords_diagnostics` | Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT. |
| `google_ads_keywords_raw` | Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT. |
| `google_ads_performance` | Daily performance breakdown: cost, impressions, clicks, conversions, revenue per day. |
| `google_ads_changes` | Change history / audit log: who changed what in the account and when. |
| `google_ads_campaign_update_status` | Pause, enable or remove one or more Google Ads campaigns. |
| `google_ads_campaign_update_budget` | Update the daily budget of a campaign. |
| `google_ads_ad_group_update_status` | Pause, enable or remove ad groups. |
| `google_ads_ad_update_status` | Pause, enable or remove ads. Each entry needs ad_group_id + ad_id because the ad resource is keyed by both (customers/X/adGroupAds/{ad_group_id}~{ad_id}). Bulk support: accepts customer_ids for batched execution. |
| `google_ads_keyword_update_status` | Pause, enable or remove keywords. |
| `google_ads_keyword_update_bid` | Update max CPC for one or more keywords. |
| `google_ads_campaign_budget_create` | Create a campaign_budget. Required to create a campaign. Amount is daily, in account currency unit (50 = R$50/day). Bulk support: accepts customer_ids for batched execution. |
| `google_ads_campaign_create` | Create a Google Ads campaign. Defaults to channel_type=SEARCH, status=PAUSED (safe), bidding_strategy=MANUAL_CPC. Provide budget_id from google_ads_campaign_budget_create. Declares no EU political advertising by defau… |
| `google_ads_ad_group_create` | Create an ad group inside a campaign. |
| `google_ads_keyword_add` | Add positive keywords to an ad group. |
| `google_ads_negative_keyword_add` | Add negative keywords at campaign or ad group scope. |
| `google_ads_responsive_search_ad_create` | Create a Responsive Search Ad (RSA) inside an ad group. |
| `google_ads_sitelinks` | List sitelink assets in the account and where they are attached (campaign / account / ad group level), with each link's resource_name (pass it to google_ads_sitelink_remove) and status. |
| `google_ads_sitelink_create` | Create sitelink extensions and attach them to a campaign (default), the whole account (scope=customer) or an ad group. |
| `google_ads_sitelink_remove` | Detach sitelinks from a campaign / account / ad group. |

---

## Pricing

Free.

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_google_ads` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
