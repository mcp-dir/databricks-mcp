# Ferramentas

Databricks expõe 11 ferramentas.

### 1. `databricks_list_accounts`
**Input**: `account` (opcional)

Lista os workspaces Databricks conectados a este install — host, label.

### 2. `databricks_current_user`
**Input**: `account` (opcional)

Identifica o usuário do PAT no workspace (whoami via SCIM Me).

### 3. `databricks_list_warehouses`
**Input**: `account` (opcional)

Lista os SQL warehouses do workspace (id, name, state, cluster_size, warehouse_type).

### 4. `databricks_get_warehouse`
**Input**: `ids`, `account` (opcional)

Detalha um ou mais SQL warehouses por id.

### 5. `databricks_run_sql`
**Input**: `statement`, `warehouse_id` (opcional), `catalog` (opcional), `schema` (opcional), `parameters` (opcional), `row_limit` (opcional), `wait_timeout` (opcional), `on_wait_timeout` (opcional), `account` (opcional), `warehouse_ids` (opcional)

Executa uma instrução SQL num SQL warehouse (Statement Execution API).

### 6. `databricks_get_statement`
**Input**: `statement_ids`, `account` (opcional)

Status + resultado de um ou mais statements por id (polling de queries longas que voltaram PENDING/RUNNING do run_sql).

### 7. `databricks_cancel_statement`
**Input**: `statement_ids`, `account` (opcional)

Cancela um ou mais statements em execução por id.

### 8. `databricks_list_catalogs`
**Input**: `account` (opcional)

Lista os catálogos do Unity Catalog visíveis ao PAT (name, comment, owner).

### 9. `databricks_list_schemas`
**Input**: `catalog_name`, `account` (opcional)

Lista os schemas (databases) de um catálogo Unity.

### 10. `databricks_list_tables`
**Input**: `catalog_name`, `schema_name`, `account` (opcional)

Lista as tabelas de um schema Unity (name, table_type, data_source_format).

### 11. `databricks_get_table`
**Input**: `full_names`, `account` (opcional)

Detalha uma ou mais tabelas (colunas, tipos) por nome completo `catalog.schema.table`.

## Prompts de exemplo

```
Liste meus SQL warehouses do Databricks
Rode: SELECT count(*) FROM samples.tpch.lineitem
Quais catálogos e tabelas existem no Unity Catalog?
```
