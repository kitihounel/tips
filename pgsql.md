# PostgreSQL

- [psql](#psql)
- [Queries](#queries)

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
