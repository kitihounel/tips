# Statistics

- [Statistics system](#statistics-system)
- [Statistics of SQL planning and execution](#statistics-of-sql-planning-and-execution)

## Statistics system

PostgreSQL's cumulative statistics system ([link](https://www.postgresql.org/docs/current/monitoring-stats.html))
supports collection and reporting of information about server activity.

For example, the following query to get the numbers of live and dead rows in a table returns only 0s:

```sql
select n_live_tup, n_dead_tup, schemaname, relname from pg_stat_all_tables;
```

##  Statistics of SQL planning and execution

The `pg_stat_statements` module provides a means for tracking planning and execution statistics of all SQL statements
executed by a server.

The module documentation is available [here](https://www.postgresql.org/docs/current/pgstatstatements.html).
