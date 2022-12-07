# PostgreSQL

- [psql](#psql)
- [Queries](#queries)
- [Template DB](#template-databases)

## psql

### List active connections

```sql
select * from pg_stat_activity;
```

If you would like to limit it to just one database, you can use:

```sql
select * from pg_stat_activity where datname = 'dbname';
```

Source: https://stackoverflow.com/questions/27435839/how-to-list-active-connections-on-postgresql

### List installed extensions in a db

```sh
\dx
```

Or

```sql
select * from pg_extension;
```

To see all available extensions on the server:

```sql
select * from pg_available_extensions;
```

## Enable UUID extension

```sql
create extension if not exists "uuid-ossp";
```

This will give you access to functions `uuid_generate_v4()` and `uuid_generate_v1()`.

## Queries

### Estimation of the number of rows in a table

```sql
select reltuples::bigint as estimate from pg_class where oid = 'schema_name.table_name'::regclass;
```

Source: https://wiki.postgresql.org/wiki/Count_estimate

## Template databases

As the names indicate, those are template databases for creating new databases.

`template1` is the one used by default. You can alter / add / remove objects there to affect every newly created DB. `CREATE DATABASE` basically makes a copy of it on the file level (very fast) to create a new instance.

`template0` starts out being the same and should never be changed - to provide a virgin template with original settings.

Their role is described in detail in the chapter [Template Databases](https://www.postgresql.org/docs/current/manage-ag-templatedbs.html) in the manual.

But you can use any database of the same cluster as template with the `TEMPLATE` keyword - as long as there are no open connections to it. This is useful to populate new databases quickly.
