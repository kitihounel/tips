# Extensions

- [List installed extensions in a database](#list-installed-extensions-in-a-database)
- [List available extensions on the server](#list-available-extensions-on-the-server)
- [Enable UUID extension](#enable-uuid-extension)

## List extensions

### List installed extensions in a database

With `psql`.

```sh
\dx
```

Using a SQL query.

```sql
select * from pg_extension;
```

### List available extensions on the server

```sql
select * from pg_available_extensions;
```

## Enable UUID extension

```sql
create extension if not exists "uuid-ossp";
```

This will give you access to functions `uuid_generate_v4()` and `uuid_generate_v1()`.
