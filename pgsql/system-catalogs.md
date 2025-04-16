# System catalog

- [Introduction to system catalogs](#introduction-to-system-catalogs)
- [Shared system catalogs](#shared-system-catalogs)
- [Activity monitoring](#activity-monitoring)

## Introduction to system catalogs

- Robert Haas talk, available on [YouTube](https://www.youtube.com/watch?v=3Tfcmq2IA6k).
- Introductory article on [DBI](https://www.dbi-services.com/blog/the-postgresql-shared-global-catalog).
- [System views](https://www.postgresql.org/docs/current/views.html).

## The `name` type

PostgreSQL system tables use a type named `name` to store system object names. It is equivalent to a 64-byte C-string.

One can get more information with the meta-command:

```txt
# \dT+ name
                                                    List of data types
   Schema   | Name | Internal name | Size | Elements |  Owner   | Access privileges |                 Description
------------+------+---------------+------+----------+----------+-------------------+---------------------------------------------
 pg_catalog | name | name          | 64   |          | postgres |                   | 63-byte type for storing system identifiers
(1 row)
```

This output comes from this [SO](https://dba.stackexchange.com/a/217538) answer.

## Shared system catalogs

Most of system catalogs are database-specific, but some are shared by all the databases in the cluster.

- Roles (`pg_authid`, `pg_auth_members`, `pg_db_role_settings`).
- Databases (`pg_database`).
- Tablespaces (`pg_tablespace`).
- Procedural language templates (`pg_pltemplate`).
- Dependencies and comments on shared objects (`pg_shdepend`, `pg_shdescription`).

## Activity monitoring

### `pg_stat_activity`

For each server backend:

- the database OID and name;
- the process PID;
- the user OID and name;
- the application name supplied by the client;
- the client address, hostname, and port;
- the times at which the backend, transaction, and query began;
- whether or not the backend is currently waiting;
- and the text of the current query.

### `pg_locks`

- All heavy-weight locks, both granted and awaited, with the exception of granted tuple locks.
- Indicates the locked object, which may be a relation, page, tuple, virtualxid, transaction ID, or other database object,
  plus the lock mode, the PID of the locker, and whether or not the lock is granted.
- Does not include information on lightweight locks or spinlocks.

#### The `virtualxid` column

This column is available in the `pg_locks` table. Every transaction has a virtual ID. It is only when the transaction
modifies the database that its is assigned a real `txid`.

### Statistics

- `pg_stat_database` (database stats).
- `pg_stat_all_tables`.
- `pg_statio_all_tables`.

There are other tables and views. See the dedicated [page](https://www.postgresql.org/docs/current/monitoring-stats.html).
