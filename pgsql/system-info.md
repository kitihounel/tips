# System information

- [Shared preloaded libraries](#shared-preloaded-libraries)
- [Database creation date](#database-creation-date)

## Shared preloaded libraries

Run the following query

```sql
SELECT current_setting('shared_preload_libraries');
```

Or if you are using psql:

```sh
show shared_preload_libraries ;
```

Note that if you don't have sufficient permissions, the query will fail with the following message:
`ERROR:  must be superuser or a member of pg_read_all_settings to examine "shared_preload_libraries"`.

## Database creation date

```sql
SELECT (pg_stat_file('base/' || oid ||'/PG_VERSION')).modification, datname FROM pg_database;
```

You need to be superuser to use that command.

Source: [SO](https://stackoverflow.com/a/30308875).

For more information about `pg_stat_file`, see PostgreSQL [doc](https://www.postgresql.org/docs/9.5/functions-admin.html).
