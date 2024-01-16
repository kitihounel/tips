# nano

- [Configuration](#configuration)
- [Line numbers](#show-line-numbers)
- [Space and tabs](#use-spaces-instead-of-tabs)
- [Undo-redo](#undo-redo)

## Configuration

The *nanorc* file contains the default settings for **nano**. The file should be in Unix format, not in DOS or Mac format. During startup, **nano** will first read the system-wide settings, from **/etc/nanorc** (the exact path might be different on your system), and then the user-specific settings, either from **~/.nanorc** or from `$XDG_CONFIG_HOME/nano/nanorc` or from **~/.config/nano/nanorc**, whichever is encountered first.

[Source](https://www.nano-editor.org/dist/v2.9/nanorc.5.html).

## Show line numbers

```
set linenumbers
```

[Source](https://askubuntu.com/questions/73444/how-to-show-line-numbering-in-nano-when-opening-a-file).

## Use spaces instead of tabs

```
set tabsize 4
set tabstospaces
```

If you already got a file with tabs and want to convert them to spaces i recommend the **expand** command (shell):

```bash
expand --tabs=4 input.py > output.py
```

[Source](https://stackoverflow.com/questions/11173769/how-to-make-the-tab-character-4-spaces-instead-of-8-spaces-in-nano).

## Undo-redo

**Alt+U** is used to undo anything in the nano editor. **Alt+E** is used to redo anything in the nano editor.

[Source](https://monovm.com/blog/how-to-undo-in-nano-editor/).
