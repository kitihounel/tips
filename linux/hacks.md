# Hacks

- [Overwrite file preserving permissions](#overwrite-file-preserving-permissions)

## Overwrite file preserving permissions

```
dd if=<source file path> of=<target file path>
```

By default, `dd` prints its status message to `stderr`. If you have GNU `dd`, you can do:

```
dd if=<source file path> of=<target file path> status=none
```

**Note:** The `dd` command can also be used to copy a file without copying its mode.

**Source:** [StackOverflow](https://unix.stackexchange.com/a/428349).
