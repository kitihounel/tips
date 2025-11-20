# Hacks

- [Overwrite file preserving permissions](#overwrite-file-preserving-permissions)
- [Get permissions for all path components](#get-permissions-for-all-path-components)

## Overwrite file preserving permissions

```sh
dd if=<source file path> of=<target file path>
```

By default, `dd` prints its status message to `stderr`. If you have GNU `dd`, you can do:

```sh
dd if=<source file path> of=<target file path> status=none
```

**Note:** The `dd` command can also be used to copy a file without copying its mode.

**Source:** [StackOverflow](https://unix.stackexchange.com/a/428349).

## Get permissions for all path components

The `namei` command can be used to display the permissions, ownership, and other details for each component
in the specified path, starting from the root directory.

```sh
namei -l /absolute/path/to/file
```
