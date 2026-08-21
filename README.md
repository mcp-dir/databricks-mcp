# Databricks

### Databricks para Claude, ChatGPT e agentes de IA

Seu Lakehouse Databricks por linguagem natural: rode SQL nos SQL warehouses, acompanhe queries longas, e explore o Unity Catalog (catálogos, schemas, tabelas e colunas), via API REST oficial do workspace. Conecte com a URL do seu workspace e um Personal Access Token (PAT).

- 📊 **11 ferramentas**
- ✏️ **Leitura e escrita**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `Databricks` e **URL** `https://api.mcp.ai/p_databricks`.

### Cursor

[➕ Instalar Databricks no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=databricks&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9kYXRhYnJpY2tzIn0=)

### VS Code (Copilot Chat)

[➕ Instalar Databricks no VS Code](vscode:mcp/install?name=databricks&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_databricks%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_databricks
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Liste meus SQL warehouses do Databricks
Rode: SELECT count(*) FROM samples.tpch.lineitem
Quais catálogos e tabelas existem no Unity Catalog?
```

---

## 11 ferramentas disponíveis

| Tool | Descrição |
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

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Grátis.

---

## Privacidade & LGPD

- **Sub-processadores**: Databricks, o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_databricks`.


---

## Suporte

- 📧 [databricks@mcp.ai](mailto:databricks@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/databricks-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_databricks` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
