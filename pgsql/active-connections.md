# Active connections

To list active conections to the server, run:

```sql
select * from pg_stat_activity;
```

If you would like to limit it to just one database, you can use:

```sql
select * from pg_stat_activity where datname = 'dbname';
```

Source: [SO](https://stackoverflow.com/questions/27435839/how-to-list-active-connections-on-postgresql).
