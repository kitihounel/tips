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

## Queries

### Estimation of the number of rows in a table

```sql
select reltuples::bigint as estimate from pg_class where oid = 'schema_name.table_name'::regclass;
```

Source: https://wiki.postgresql.org/wiki/Count_estimate
