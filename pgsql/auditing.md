# Auditing

- [Simple audit system](#simple-audit-system)
- [pgAudit](#pgaudit)

## Simple audit system

This [article](https://supabase.com/blog/postgres-audit) on **Supabase**
blog presents how to build an audit system for a database.

There is GitHub [repo](https://github.com/supabase/supa_audit) with the
source code.

### IMPORTANT

Please, read the whole article to learn about its limitations and when it
will be better to use **pgAudit**.

## pgAudit

[pgAudit](https://www.pgaudit.org) provides detailed session and/or object
audit logging via the standard logging facility provided by PostgreSQL.
The goal of PostgreSQL Audit to provide the tools needed to produce audit
logs required to pass certain government, financial, or ISO certification
audits.

An introduction article by **ScaleGrid** is available
[here](https://scalegrid.io/blog/auditing-postgresql-using-pgaudit/).
