# Template databases

As the names suggest, those are template for creating new databases.

`template1` is the one used by default. You can alter / add / remove objects there to affect every newly created DB. `CREATE DATABASE` basically makes a copy of it on the file level (very fast) to create a new instance.

`template0` starts out being the same and should never be changed - to provide a virgin template with original settings.

Their role is described in detail in the chapter [Template Databases](https://www.postgresql.org/docs/current/manage-ag-templatedbs.html) in the manual.

But you can use any database of the same cluster as template with the `TEMPLATE` keyword - as long as there are no open connections to it. This is useful to populate new databases quickly.
