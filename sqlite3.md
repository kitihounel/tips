# sqlite3

- [Query results display format](#query-results-display-format)

## Query results display format

Use the `.mode` **dot command** to set how query results are displayed

If you want your query results to be displayed like a table, use the `column` argument.

```sh
.mode column
```

If you want the **extended** display (similar to the one available in `psql`), use the `line` argument.

```sh
.mode line
```

There are other possibilities, like `box` and `qbox`.

If you also want the column names to be displayed, use the `.headers` command

```sh
.headers on
```
