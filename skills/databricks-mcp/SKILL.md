---
name: databricks-mcp
description: Skill da REST API do Databricks na MCP.AI: 11 endpoints em /api/databricks. Seu Lakehouse Databricks por linguagem natural: rode SQL nos SQL warehouses, acompanhe queries longas, e explore o Unity Catalog (catálogos, schemas, tabelas e colunas), via API REST oficial do workspace. Conecte com a URL do seu workspace e um Personal Access Token (PAT). Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# Databricks — REST API skill

Você tem acesso à **Databricks** REST API na MCP.AI.

> Seu Lakehouse Databricks por linguagem natural: rode SQL nos SQL warehouses, acompanhe queries longas, e explore o Unity Catalog (catálogos, schemas, tabelas e colunas), via API REST oficial do workspace. Conecte com a URL do seu workspace e um Personal Access Token (PAT).

## Base URL

```
https://api.mcp.ai/api/databricks
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
curl -X POST https://api.mcp.ai/api/databricks/cancel/statement \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"statement_ids":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/databricks/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (11)

#### `databricks_cancel_statement`

Cancela um ou mais statements em execução por id. _(POST /api/databricks/cancel/statement)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `statement_ids` | string[] | Sim | Ids dos statements a cancelar. |
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_current_user`

Identifica o usuário do PAT no workspace (whoami via SCIM Me). _(POST /api/databricks/current/user)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_get_statement`

Status + resultado de um ou mais statements por id (polling de queries longas que voltaram PENDING/RUNNING do run_sql). _(POST /api/databricks/get/statement)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `statement_ids` | string[] | Sim | Ids dos statements (statement_id devolvido pelo run_sql). |
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_get_table`

Detalha uma ou mais tabelas (colunas, tipos) por nome completo `catalog.schema.table`. _(POST /api/databricks/get/table)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `full_names` | string[] | Sim | Nomes completos das tabelas (ex.: ['samples.tpch.lineitem']). |
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_get_warehouse`

Detalha um ou mais SQL warehouses por id. _(POST /api/databricks/get/warehouse)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Ids dos warehouses (ex.: ['abc123']). |
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_list_accounts`

Lista os workspaces Databricks conectados a este install — host, label. _(POST /api/databricks/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_list_catalogs`

Lista os catálogos do Unity Catalog visíveis ao PAT (name, comment, owner). _(POST /api/databricks/list/catalogs)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_list_schemas`

Lista os schemas (databases) de um catálogo Unity. _(POST /api/databricks/list/schemas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `catalog_name` | string | Sim | Nome do catálogo Unity. |
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_list_tables`

Lista as tabelas de um schema Unity (name, table_type, data_source_format). _(POST /api/databricks/list/tables)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `catalog_name` | string | Sim | Nome do catálogo Unity. |
| `schema_name` | string | Sim | Nome do schema (database). |
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_list_warehouses`

Lista os SQL warehouses do workspace (id, name, state, cluster_size, warehouse_type). _(POST /api/databricks/list/warehouses)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |

#### `databricks_run_sql`

Executa uma instrução SQL num SQL warehouse (Statement Execution API). _(POST /api/databricks/run/sql)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `statement` | string | Sim | SQL a executar. Parâmetros nomeados com `:nome` casam com `parameters[].name`. |
| `warehouse_id` | string | Não | Id do SQL warehouse. Omitido = escolhe um RUNNING (veja databricks_list_warehouses). |
| `catalog` | string | Não | Catálogo Unity padrão da query. |
| `schema` | string | Não | Schema (database) padrão da query. |
| `parameters` | object[] | Não | Parâmetros da query (recomendado vs interpolar na string). |
| `row_limit` | integer | Não | Limite de linhas retornadas (alternativa ao LIMIT no SQL). |
| `wait_timeout` | string | Não | Espera síncrona: '0s' (retorna já) ou '5s'..'50s' (default '30s'). |
| `on_wait_timeout` | string | Não | Ao estourar o wait_timeout: CONTINUE (default) segue rodando, CANCEL cancela. (CONTINUE, CANCEL) |
| `account` | string | Não | Quando há múltiplos workspaces Databricks conectados: host ou label da conexão. Veja databricks_list_accounts. |
| `warehouse_ids` | string[] | Não | Bulk mode: multiple values for warehouse_id |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_databricks` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
