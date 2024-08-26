# Privileges

## Usage privilege

From the official [documentation](https://www.postgresql.org/docs/current/ddl-priv.html):

> For procedural languages, allows the use of the specified language for the creation of functions in that language. This is the only type of privilege that is applicable to procedural languages.\
> For schemas, allows access to objects contained in the specified schema (assuming that the objects own privilege requirements are also met). Essentially this allows the grantee to "look up" objects within the schema. Without this permission, it is still possible to see the object names, e.g. by querying the system tables. Also, after revoking this permission, existing backends might have statements that have previously performed this lookup, so this isn't a completely secure way to prevent object access.\
> For sequences, this privilege allows the use of the currval and nextval functions.\
> For foreign-data wrappers, this privilege enables the grantee to create new servers using that foreign-data wrapper.\
> For servers, this privilege enables the grantee to create, alter, and drop his own user's user mappings associated with that server. Also, it enables the grantee to query the options of the server and associated user mappings.

Also, if a user has the **USAGE** privilege on a schema, he will be able to create objects in that schema. Since all users by default have access to the public schema, it is better to remove this access after the database creation:

```sql
CREATE DATABASE mydb OWNER myuser;
REVOKE CONNECT ON DATABASE mydb FROM public;
\c mydb myuser;
REVOKE USAGE ON SCHEMA public FROM public;
```

This SO [answer](https://stackoverflow.com/a/17355059/14972608) can be useful.

To get detailed information about privileges in a database, you can query the `usage_privileges` and `role_table_grants` views of the `information_schema`. More details are provided in the information schema [doc](https://www.postgresql.org/docs/current/information-schema.html).
