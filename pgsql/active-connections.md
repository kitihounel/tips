# Connections

- [List active connections](#list-active-connections)
- [Terminate connections](#terminate-connections)

## List active connections

To list active conections to the server, run:

```sql
select * from pg_stat_activity;
```

If you would like to limit it to just one database, you can use:

```sql
select * from pg_stat_activity where datname = 'dbname';
```

Source: [SO](https://stackoverflow.com/questions/27435839/how-to-list-active-connections-on-postgresql).

## Terminate connections

If you need to terminate connections, you can use the following query:

```sql
select
  pg_terminate_backend(procpid)
from
  pg_stat_activity
where
  procpid != pg_backend_pid() and <your condition goes here>;
```

It can be used for example, to delete connections that does not supply an application name by using a CRON.
