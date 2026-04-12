# Bash history cheatsheet

- [Shortcuts](#shortcuts)
- [Other tips](#other-tips)

## Shortcuts

| Shortcut      | Usage                                                                                     |
| --------------| ------------------------------------------------------------------------------------------|
| `!!`          | Reexecute last command line                                                               |
| `!:0`         | Expand to last command                                                                    |
| `!^`          | First argument of last command line                                                       |
| `!$`          | Last argument of last command line                                                        |
| `!n`          | Expand nth command in history                                                             |
| `!-n`         | Expand nth most recent command                                                            |
| `!<command>`  | Expand most recent invocation of `<command>`                                              |
| `!N:p`        | Recall nth command line without executing (seems to only work with begative values of n)  |

## Other tips

### Settings

```bash
shopt -s histverify # Expand without executing
```

### Search in history

To search in history, use `Ctrl+R`. To exit the search mode, use `Ctrl+A`.

### Go to start or end of history

You can use chevrons to move to the start or end of the history: `Ctrl+>` or `Ctrl+<`. To exit, use `Ctrl+C` .
