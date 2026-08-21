# Ferramentas

Google Ads expõe 29 ferramentas.

### 1. `google_ads_list_accounts`
**Input**: `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

List all Google Ads MCCs and ALL customer accounts the OAuth token can access (via customers:listAccessibleCustomers — not just hierarchy of the MCC).

### 2. `google_ads_status`
**Input**: `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Without account: overview of all Google Ads MCCs and customer_ids.

### 3. `google_ads_account`
**Input**: `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Get Google Ads account info: name, currency, timezone for a customer (uses account + customer_id to resolve scope).

### 4. `google_ads_campaigns`
**Input**: `status` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

List Google Ads campaigns with status and budgets.

### 5. `google_ads_today`
**Input**: `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Today Google Ads performance: cost, impressions, clicks, conversions, ROAS per campaign plus _summary.

### 6. `google_ads_roas`
**Input**: `since` (opcional), `until` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

ROAS for a date range (defaults to current month).

### 7. `google_ads_ads`
**Input**: `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

List enabled ads with type, status, campaign name and ad_group_ad.policy_summary (approval_status, review_status, policy_topic_entries) — answers "why is my ad not serving?" without opening the Google Ads UI.

### 8. `google_ads_keywords_keywords`
**Input**: `query` (opcional), `campaign_id` (opcional), `ad_group_id` (opcional), `days` (opcional), `account` (opcional), `customer_id` (opcional), `campaign_ids` (opcional), `ad_group_ids` (opcional), `customer_ids` (opcional)

Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT.

### 9. `google_ads_keywords_search_terms`
**Input**: `query` (opcional), `campaign_id` (opcional), `ad_group_id` (opcional), `days` (opcional), `account` (opcional), `customer_id` (opcional), `campaign_ids` (opcional), `ad_group_ids` (opcional), `customer_ids` (opcional)

Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT.

### 10. `google_ads_keywords_status`
**Input**: `query` (opcional), `campaign_id` (opcional), `ad_group_id` (opcional), `days` (opcional), `account` (opcional), `customer_id` (opcional), `campaign_ids` (opcional), `ad_group_ids` (opcional), `customer_ids` (opcional)

Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT.

### 11. `google_ads_keywords_diagnostics`
**Input**: `query` (opcional), `campaign_id` (opcional), `ad_group_id` (opcional), `days` (opcional), `account` (opcional), `customer_id` (opcional), `campaign_ids` (opcional), `ad_group_ids` (opcional), `customer_ids` (opcional)

Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT.

### 12. `google_ads_keywords_raw`
**Input**: `query` (opcional), `campaign_id` (opcional), `ad_group_id` (opcional), `days` (opcional), `account` (opcional), `customer_id` (opcional), `campaign_ids` (opcional), `ad_group_ids` (opcional), `customer_ids` (opcional)

Keyword analytics, search terms, status/policy diagnostics, auction diagnostics, or custom GAQL SELECT.

### 13. `google_ads_performance`
**Input**: `days` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Daily performance breakdown: cost, impressions, clicks, conversions, revenue per day.

### 14. `google_ads_changes`
**Input**: `since` (opcional), `until` (opcional), `days` (opcional), `limit` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Change history / audit log: who changed what in the account and when.

### 15. `google_ads_campaign_update_status`
**Input**: `campaign_ids`, `status`, `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional)

Pause, enable or remove one or more Google Ads campaigns.

### 16. `google_ads_campaign_update_budget`
**Input**: `campaign_id`, `amount`, `account` (opcional), `customer_id` (opcional), `campaign_ids` (opcional), `customer_ids` (opcional)

Update the daily budget of a campaign.

### 17. `google_ads_ad_group_update_status`
**Input**: `ad_group_ids`, `status`, `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional)

Pause, enable or remove ad groups.

### 18. `google_ads_ad_update_status`
**Input**: `ads`, `status`, `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Pause, enable or remove ads. Each entry needs ad_group_id + ad_id because the ad resource is keyed by both (customers/X/adGroupAds/{ad_group_id}~{ad_id}). Bulk support: accepts customer_ids for batched execution.

### 19. `google_ads_keyword_update_status`
**Input**: `keywords`, `status`, `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Pause, enable or remove keywords.

### 20. `google_ads_keyword_update_bid`
**Input**: `keywords`, `cpc_bid`, `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Update max CPC for one or more keywords.

### 21. `google_ads_campaign_budget_create`
**Input**: `name`, `amount`, `delivery_method` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Create a campaign_budget. Required to create a campaign. Amount is daily, in account currency unit (50 = R$50/day). Bulk support: accepts customer_ids for batched execution.

### 22. `google_ads_campaign_create`
**Input**: `name`, `budget_id`, `channel_type` (opcional), `bidding_strategy` (opcional), `status` (opcional), `eu_political_ad` (opcional), `account` (opcional), `customer_id` (opcional), `budget_ids` (opcional), `customer_ids` (opcional)

Create a Google Ads campaign. Defaults to channel_type=SEARCH, status=PAUSED (safe), bidding_strategy=MANUAL_CPC. Provide budget_id from google_ads_campaign_budget_create. Declares no EU political advertising by defau…

### 23. `google_ads_ad_group_create`
**Input**: `campaign_id`, `name`, `type` (opcional), `status` (opcional), `cpc_bid` (opcional), `account` (opcional), `customer_id` (opcional), `campaign_ids` (opcional), `customer_ids` (opcional)

Create an ad group inside a campaign.

### 24. `google_ads_keyword_add`
**Input**: `ad_group_id`, `keywords`, `status` (opcional), `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional), `ad_group_ids` (opcional), `customer_ids` (opcional)

Add positive keywords to an ad group.

### 25. `google_ads_negative_keyword_add`
**Input**: `scope`, `target_id`, `keywords`, `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional), `target_ids` (opcional), `customer_ids` (opcional)

Add negative keywords at campaign or ad group scope.

### 26. `google_ads_responsive_search_ad_create`
**Input**: `ad_group_id`, `headlines`, `descriptions`, `final_urls`, `path1` (opcional), `path2` (opcional), `status` (opcional), `account` (opcional), `customer_id` (opcional), `ad_group_ids` (opcional), `customer_ids` (opcional)

Create a Responsive Search Ad (RSA) inside an ad group.

### 27. `google_ads_sitelinks`
**Input**: `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

List sitelink assets in the account and where they are attached (campaign / account / ad group level), with each link's resource_name (pass it to google_ads_sitelink_remove) and status.

### 28. `google_ads_sitelink_create`
**Input**: `scope` (opcional), `target_id` (opcional), `sitelinks`, `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional), `target_ids` (opcional), `customer_ids` (opcional)

Create sitelink extensions and attach them to a campaign (default), the whole account (scope=customer) or an ad group.

### 29. `google_ads_sitelink_remove`
**Input**: `link_resource_names`, `partial_failure` (opcional), `account` (opcional), `customer_id` (opcional), `customer_ids` (opcional)

Detach sitelinks from a campaign / account / ad group.

## Prompts de exemplo

```
Liste minhas contas Google Ads acessíveis pela MCC
Quanto gastei hoje em Google Ads e qual o ROAS por campanha?
Top 10 palavras-chave por custo nos últimos 7 dias
```
