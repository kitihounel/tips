# Count Queries

PostgreSQL is not very good at counting. But there are many good workarounds.

## Estimation of the number of rows in a table

```sql
select reltuples::bigint as estimate from pg_class where oid = 'schema_name.table_name'::regclass;
```

Source: [PostgreSQL wiki](https://wiki.postgresql.org/wiki/Count_estimate).

## Faster PostgreSQL counting

There is a very good article by Joe Nelson about this topic. See [here](https://www.citusdata.com/blog/2016/10/12/count-performance).
