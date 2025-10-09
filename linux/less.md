# less

- [Secure mode](#secure-mode)
- [ASCII escape sequences](#ascii-escape-sequences)


## Secure mode

`less` can run in a secure mode that disables some features. To enable this mode, you need to create an environment variable named
`LESSSECURE`.

See the manpage for more details.

## ASCII escape sequences

There is an `-R` option that allows `less` to interpret ASCII escape sequences. This can be useful when you need to read log
files which can contain escape sequence to help identify parts in log entries.
