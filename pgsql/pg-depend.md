# pg-depend

The catalog `pg_depend` records the dependency relationships between database objects. This information allows `DROP` commands to find which other objects must be dropped by `DROP CASCADE` or prevent dropping in the `DROP RESTRICT` case.

Read more [here](https://www.postgresql.org/docs/current/catalog-pg-depend.html).
