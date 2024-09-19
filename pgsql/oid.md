# Object Identifiers

## Official doc

- Dedicated page in PgSQL [doc](https://www.postgresql.org/docs/current/datatype-oid.html).

## Get table OID

Read this [answer](https://stackoverflow.com/a/10956124/14972608) on SO.

There are two methods:

```sql
SELECT 'myschema.mytbl'::regclass::oid;
```

```sql
SELECT to_regclass('myschema.mytbl')::oid;
```

The `to_regclass` function returns `NULL` if the relation does not exist.
