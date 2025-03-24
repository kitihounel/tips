# Indexes

- [List indexes](#list-indexes)

# List indexes

The `pg_indexes` view allows you to access useful information on each index in the PostgreSQL database.
It consists of five columns:

- `schemaname`: stores the name of the schema that contains tables and indexes.
- `tablename`: indicates the name of the table to which the index belongs.
- `indexname`: represents the name of the index.
- `tablespace`: identifies the name of the tablespace that contains indexes.
- `indexdef`: contains the index definition command in the form of CREATE INDEX statement.

You can also use the `\d` from `psql` to get all information about a table including the table's structure,
indexes, constraints, and triggers.

**Source:** https://neon.tech/postgresql/postgresql-indexes/postgresql-list-indexes.
