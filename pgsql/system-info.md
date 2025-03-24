# System information

- [Shared preloaded libraries](#shared-preloaded-libraries)

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
