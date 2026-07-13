# grep

- [Print lines before and after matches](#print-lines-before-and-after-matches)
- [Stop a first match](#stop-a-first-match)

## Print lines before and after matches

There are the `A`, `B`, and `C` options available to perform this task.
See the `grep` man page for complete reference.

# Stop a first match

To make grep stop after the first match, use the `-m 1` or `--max-count=1` flag.

```sh
grep -m 1 'pattern' filename.txt
```

To make `grep` display only the matched text and not the whole line, use the `-o` flag.
