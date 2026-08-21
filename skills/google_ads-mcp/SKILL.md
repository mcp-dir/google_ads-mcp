---
name: google_ads-mcp
description: Skill da REST API do Google Ads na MCP.AI: 25 endpoints em /api/google_ads. Gestão completa de Google Ads: leitura (campanhas, performance, ROAS, keywords, termos de busca) e escrita (pausar/ativar/remover campanhas, ad groups, ads e keywords, ajustar orçamento e lance, criar budget, campanha, ad group, keywords positivas/negativas e RSAs). Você fornece developer token, OAuth client_id/secret, refresh_token e MCC, sem etapa OAuth no servidor. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# Google Ads — REST API skill

Você tem acesso à **Google Ads** REST API na MCP.AI.

> Gestão completa de Google Ads: leitura (campanhas, performance, ROAS, keywords, termos de busca) e escrita (pausar/ativar/remover campanhas, ad groups, ads e keywords, ajustar orçamento e lance, criar budget, campanha, ad group, keywords positivas/negativas e RSAs). Você fornece developer token, OAuth client_id/secret, refresh_token e MCC, sem etapa OAuth no servidor.

## Base URL

```
https://api.mcp.ai/api/google_ads
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/google_ads/accounts \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/google_ads/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (25)

#### `google_ads_list_accounts`

Listar MCCs e TODOS os customer accounts acessíveis pelo OAuth token _(POST /api/google_ads/accounts)_

#### `google_ads_status`

Overview de MCCs e customer_ids (sem account). _(POST /api/google_ads/status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |

#### `google_ads_account`

Info do customer: nome, moeda, timezone _(POST /api/google_ads/customers/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |

#### `google_ads_campaigns`

Listar campanhas com status e orçamentos _(POST /api/google_ads/customers/campaigns)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `status` | string | Não | Filtro por status (default ENABLED) (ENABLED, PAUSED) |

#### `google_ads_today`

Performance de hoje: custo, impressões, cliques, conversões, ROAS por campanha + _summary _(POST /api/google_ads/customers/today)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |

#### `google_ads_roas`

ROAS por período (default mês corrente). _(POST /api/google_ads/customers/roas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `since` | string | Não | Início YYYY-MM-DD (default: primeiro dia do mês) |
| `until` | string | Não | Fim YYYY-MM-DD (default: hoje) |

#### `google_ads_ads`

Listar ads habilitados com tipo, status, nome da campanha e policy_summary (approval/review status) _(POST /api/google_ads/customers/ads)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |

#### `google_ads_keywords`

Keywords: métricas, search terms, status/policy (action=status), diagnóstico de leilão / Quality Score (action=diagnostics) ou GAQL raw _(POST /api/google_ads/customers/keywords)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `action` | string | Não | Ação (default keywords). status = approval_status + system_serving_status + disapproval_reasons (responde 'por que não está servindo?'). diagnostics = Quality Score + position_estimates (top-of-page CPC) + impression_share + rank-lost vs budget-lost (responde 'é lance ou Quality Score?'). raw = GAQL SELECT customizado. (keywords, search_terms, status, diagnostics, raw) |
| `query` | string | Não | Apenas para action=raw: GAQL SELECT |
| `campaign_id` | string | Não | Apenas para action=diagnostics: filtra por uma campanha |
| `ad_group_id` | string | Não | Apenas para action=diagnostics: filtra por um ad group |
| `days` | number | Não | Apenas para action=diagnostics: 7 | 14 | 30 (default 7) |

#### `google_ads_changes`

Histórico de alterações (quem mudou o quê): campanhas, anúncios, lances, URLs, headlines, keywords, orçamentos _(POST /api/google_ads/customers/changes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `since` | string | Não | Início "YYYY-MM-DD" ou "YYYY-MM-DD HH:MM:SS". Máx 30 dias atrás. Para polling incremental, passe o timestamp da última mudança vista. |
| `until` | string | Não | Fim "YYYY-MM-DD" ou "YYYY-MM-DD HH:MM:SS" (default: agora) |
| `days` | number | Não | Janela em dias quando `since` é omitido (default 7, máx 30) |
| `limit` | number | Não | Máx de eventos (default 1000, máx 10000) |

#### `google_ads_performance`

Performance diária: custo, impressões, cliques, conversões, revenue por dia _(POST /api/google_ads/customers/performance)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `days` | number | Não | Janela em dias (default 7) |

#### `google_ads_campaign_update_status`

Pausar, ativar ou remover campanhas (REMOVED é irreversível) _(POST /api/google_ads/campaigns/update-status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `campaign_ids` | array | Sim | IDs das campanhas |
| `status` | string | Sim | Novo status (ENABLED, PAUSED, REMOVED) |
| `partial_failure` | boolean | Não | Tolera falhas parciais (default false) |

#### `google_ads_campaign_update_budget`

Ajustar o orçamento diário de uma campanha (na unidade da moeda da conta) _(POST /api/google_ads/campaigns/update-budget)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `campaign_id` | string | Sim | ID da campanha |
| `amount` | number | Sim | Novo orçamento diário (ex.: 50.5 = R$50,50) |

#### `google_ads_ad_group_update_status`

Pausar, ativar ou remover ad groups _(POST /api/google_ads/ad-groups/update-status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `ad_group_ids` | array | Sim | IDs dos ad groups |
| `status` | string | Sim | Novo status (ENABLED, PAUSED, REMOVED) |
| `partial_failure` | boolean | Não | Tolera falhas parciais |

#### `google_ads_ad_update_status`

Pausar, ativar ou remover anúncios (precisa de ad_group_id + ad_id) _(POST /api/google_ads/ads/update-status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `ads` | array | Sim | Lista de {ad_group_id, ad_id} |
| `status` | string | Sim | Novo status (ENABLED, PAUSED, REMOVED) |
| `partial_failure` | boolean | Não | Tolera falhas parciais |

#### `google_ads_keyword_update_status`

Pausar, ativar ou remover keywords (precisa de ad_group_id + criterion_id) _(POST /api/google_ads/keywords/update-status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `keywords` | array | Sim | Lista de {ad_group_id, criterion_id} |
| `status` | string | Sim | Novo status (ENABLED, PAUSED, REMOVED) |
| `partial_failure` | boolean | Não | Tolera falhas parciais |

#### `google_ads_keyword_update_bid`

Ajustar max CPC de keywords (na unidade da moeda da conta) _(POST /api/google_ads/keywords/update-bid)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `keywords` | array | Sim | Lista de {ad_group_id, criterion_id} |
| `cpc_bid` | number | Sim | Novo max CPC aplicado a todas (ex.: 1.5 = R$1,50) |
| `partial_failure` | boolean | Não | Tolera falhas parciais |

#### `google_ads_campaign_budget_create`

Criar um campaign_budget (pré-requisito de toda campanha) _(POST /api/google_ads/campaign-budgets/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `name` | string | Sim | Nome do orçamento (único na conta) |
| `amount` | number | Sim | Orçamento diário na unidade da moeda da conta |
| `delivery_method` | string | Não | Default STANDARD (STANDARD, ACCELERATED) |

#### `google_ads_campaign_create`

Criar uma campanha (default SEARCH, PAUSED, MANUAL_CPC). _(POST /api/google_ads/campaigns/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `name` | string | Sim | Nome da campanha |
| `budget_id` | string | Sim | ID do campaign_budget |
| `channel_type` | string | Não | Default SEARCH (SEARCH, DISPLAY, SHOPPING, VIDEO, PERFORMANCE_MAX) |
| `bidding_strategy` | string | Não | Default MANUAL_CPC (MANUAL_CPC, MAXIMIZE_CONVERSIONS, MAXIMIZE_CONVERSION_VALUE, MAXIMIZE_CLICKS) |
| `status` | string | Não | Default PAUSED (seguro pra campanha nova) (ENABLED, PAUSED) |

#### `google_ads_ad_group_create`

Criar um ad group dentro de uma campanha _(POST /api/google_ads/ad-groups/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `campaign_id` | string | Sim | ID da campanha |
| `name` | string | Sim | Nome do ad group |
| `type` | string | Não | Default SEARCH_STANDARD (SEARCH_STANDARD, DISPLAY_STANDARD, SHOPPING_PRODUCT_ADS, VIDEO_BUMPER, VIDEO_TRUE_VIEW_IN_STREAM) |
| `status` | string | Não | Default ENABLED (ENABLED, PAUSED) |
| `cpc_bid` | number | Não | Max CPC default do grupo (moeda da conta) |

#### `google_ads_keyword_add`

Adicionar keywords positivas a um ad group _(POST /api/google_ads/keywords/add)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `ad_group_id` | string | Sim | ID do ad group |
| `keywords` | array | Sim | Lista de {text, match_type?, cpc_bid?} |
| `status` | string | Não | Default ENABLED (ENABLED, PAUSED) |
| `partial_failure` | boolean | Não | Tolera falhas parciais |

#### `google_ads_negative_keyword_add`

Adicionar keywords negativas (campaign ou ad group) _(POST /api/google_ads/negative-keywords/add)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `scope` | string | Sim | Onde anexar (campaign, ad_group) |
| `target_id` | string | Sim | campaign_id se scope=campaign, ad_group_id se scope=ad_group |
| `keywords` | array | Sim | Lista de {text, match_type?} |
| `partial_failure` | boolean | Não | Tolera falhas parciais |

#### `google_ads_responsive_search_ad_create`

Criar um Responsive Search Ad (RSA) num ad group _(POST /api/google_ads/ads/responsive-search/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `ad_group_id` | string | Sim | ID do ad group |
| `headlines` | array | Sim | 3 a 15 headlines (cada <= 30 chars) |
| `descriptions` | array | Sim | 2 a 4 descriptions (cada <= 90 chars) |
| `final_urls` | array | Sim | Landing page(s) |
| `path1` | string | Não | Display path 1 (<= 15 chars) |
| `path2` | string | Não | Display path 2 (<= 15 chars) |
| `status` | string | Não | Default PAUSED (ENABLED, PAUSED) |

#### `google_ads_sitelinks`

Listar sitelinks e onde estão linkados (campanha / conta / ad group) _(POST /api/google_ads/sitelinks/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |

#### `google_ads_sitelink_create`

Criar sitelinks e linkar numa campanha (default), na conta ou num ad group _(POST /api/google_ads/sitelinks/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `scope` | string | Não | Onde anexar (default campaign; customer = conta inteira) (campaign, customer, ad_group) |
| `target_id` | string | Não | campaign_id ou ad_group_id; omitir se scope=customer |
| `sitelinks` | array | Sim | Lista de {link_text (<=25), final_url, description1?, description2? (<=35)} |
| `partial_failure` | boolean | Não | Tolera falhas parciais |

#### `google_ads_sitelink_remove`

Desligar sitelinks (remove só a associação; o asset fica na biblioteca) _(POST /api/google_ads/sitelinks/remove)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | MCC: mcc_id ou label da conexão (multi-MCC). Omita se houver apenas uma. |
| `customer_id` | string | Não | Customer ID (10 dígitos, hífens opcionais). Default = primeiro customer / MCC. |
| `link_resource_names` | array | Sim | resource_names das associações vindos de google_ads_sitelinks |
| `partial_failure` | boolean | Não | Tolera falhas parciais |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_google_ads` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
