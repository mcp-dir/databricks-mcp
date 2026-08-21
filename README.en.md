# Databricks

### Databricks for Claude, ChatGPT and AI agents

Your Databricks Lakehouse in natural language: run SQL on your SQL warehouses, track long-running queries, and explore Unity Catalog (catalogs, schemas, tables and columns), via the official workspace REST API. Connect with your workspace URL and a Personal Access Token (PAT).

- 📊 **11 tools**
- ✏️ **Read and write**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → name `Databricks`, URL `https://api.mcp.ai/p_databricks`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=databricks&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9kYXRhYnJpY2tzIn0=)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=databricks&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_databricks%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_databricks
```

---

## 11 tools

| Tool | Description |
|---|---|
| `databricks_list_accounts` | Lista os workspaces Databricks conectados a este install — host, label. |
| `databricks_current_user` | Identifica o usuário do PAT no workspace (whoami via SCIM Me). |
| `databricks_list_warehouses` | Lista os SQL warehouses do workspace (id, name, state, cluster_size, warehouse_type). |
| `databricks_get_warehouse` | Detalha um ou mais SQL warehouses por id. |
| `databricks_run_sql` | Executa uma instrução SQL num SQL warehouse (Statement Execution API). |
| `databricks_get_statement` | Status + resultado de um ou mais statements por id (polling de queries longas que voltaram PENDING/RUNNING do run_sql). |
| `databricks_cancel_statement` | Cancela um ou mais statements em execução por id. |
| `databricks_list_catalogs` | Lista os catálogos do Unity Catalog visíveis ao PAT (name, comment, owner). |
| `databricks_list_schemas` | Lista os schemas (databases) de um catálogo Unity. |
| `databricks_list_tables` | Lista as tabelas de um schema Unity (name, table_type, data_source_format). |
| `databricks_get_table` | Detalha uma ou mais tabelas (colunas, tipos) por nome completo `catalog.schema.table`. |

---

## Pricing

Free.

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_databricks` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
