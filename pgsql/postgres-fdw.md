# Postgres FDW extension how-to

## How-to create a readonly foreign table

We want to create a readonly view on a server (`pg-remote`) that we will
access from another server (`pg-fdw`).

We made the tests using Docker containers, this is why we used the host
`host.docker.internal` that allows us to access the host machine from
the containers.

### On the first server

The server is named `pg-remote`. We will work on the `mvcc` database.

1. Create a view named `mvcc_view`.

    ```sql
      CREATE USER mvcc_view AS SELECT * FROM mvcctable WHERE id < 1000000;
    ```

2. Create the user `fdw_user` that will be used on the second server
   to access the view.

    ```sql
    CREATE USER fdw_user WITH LOGIN PASSWORD 'password';
    ```

3. Grant the user select rights on the view.

    ```sql
    GRANT SELECT ON mvcc_view TO fdw_user;
    ```

### On the second server

The server is named `pg-fdw`. The db is named `fdw`.

1. Create the `postgres_fdw` extension in the db.

    ```sql
    CREATE EXTENSION IF NOT EXISTS postgres_fdw;
    ```

2. Create the source server

    ```sql
    CREATE SERVER fdw_server FOREIGN DATA WRAPPER postgres_fdw OPTIONS (host 'host.docker.internal', dbname 'mvcc', port '15432');
    ```

3. Grant usage on the server to the admin user.

    ```sql
    GRANT USAGE ON FOREIGN SERVER fdw_server TO admin;
    ```

4. Create a user mapping

    ```sql
    CREATE USER MAPPING FOR admin SERVER fdw_server OPTIONS (user 'fdw_user', password 'password');
    ```

5. Create the foreign table

    ```sql
    CREATE FOREIGN TABLE mvcc_view_fdw SERVER fdw_server OPTIONS (schema_name 'public', table_name 'mvcc_view');
    ```

6. To check that the view is readonly, we can try to insert a row in the table.

```sql
INSERT INTO mvcc_view_fdw VALUES (200000, 'abcd');
```

We get the following error:

```txt
ERROR:  permission denied for view mvcc_view
CONTEXT:  remote SQL command: INSERT INTO public.mvcc_view(id, val) VALUES ($1, $2)
```

#### IMPORTANT

The above command could fail because we do not specify the columns of the
foreign table. The doc says that the column is optional, but when we try
without specifying the column lis, the command fails.

## Useful commands

### Drop a foreign table

```sql
DROP FOREIGN TABLE IF EXISTS foreign_table_name;
```

### Drop a user mapping

```sql
DROP USER MAPPING IF EXISTS FOR local_user SERVER source_server;
```

### Drop a foreign server

It's better to use this one since the `cascade` option  allows to
automatically drop all objects that depend on the foreign server,
such as user mappings and foreign tables

```sql
DROP SERVER IF EXISTS source_server CASCADE;
```

## Get information from psql

- `\des[+]` List foreign servers
- `\deu[+]` List user mappings
- `\det[+]` List foreign tables
