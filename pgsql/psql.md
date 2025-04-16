# psql

- [Expanded table formatting](#expanded-table-formatting)
- [Log meta-commands queries](#log-meta-commands-queries)

## Expanded table formatting

Using the `\x` command, we can toggle expanded table formatting mode. This is useful when the width of the output
of a query is larget than the screen width.

See also the `\pset` command for more options.

## Log meta-commands queries

The `-E` options makes `psql` log the queries used by meta-commands.
