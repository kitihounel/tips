# Console font

Read this [article](https://www.linux.com/topic/desktop/how-change-your-linux-console-fonts).
The remaining of this document comes from the article.

## Finding fonts

As far as I know, there is no way to list your installed kernel fonts other
than looking in the directories they are stored in:

- `/usr/share/consolefonts` (Debian and its derivatives),
- `/lib/kbd/consolefonts` (Fedora),
- `/usr/share/kbd/consolefonts` (openSUSE),
- etc.

## Changing fonts

On Debian/Ubuntu systems you can run `sudo dpkg-reconfigure console-setup` to
set your console font, then run the `setupcon` command in your console to
activate the changes. `setupcon` is part of the `console-setup package`. If
your Linux distribution doesn’t include it, there might be a package for you at
openSUSE.

You can also edit `/etc/default/console-setup` directly. This example sets the
**Terminus Bold** font at $32$ points, which is my favorite, and restricts the width
to $80$ columns.

```txt
ACTIVE_CONSOLES="/dev/tty[1-6]"
CHARMAP="UTF-8"
CODESET="guess"
FONTFACE="TerminusBold"
FONTSIZE="16x32"
SCREEN_WIDTH="80"
```

The `FONTFACE` and `FONTSIZE` values come from the font’s filename,
`TerminusBold32x16.psf.gz`. Yes, you have to know to reverse the order for
`FONTSIZE`. Computers are so much fun. Run `setupcon` to apply the new
configuration. You can see the whole character set for your active font with
`showconsolefont`. Refer to man `console-setup` for complete options.

## Systemd

Systemd is different from `console-setup`, and you don’t need to install
anything, except maybe some extra font packages. All you do is edit
`/etc/vconsole.conf` and then reboot. On my Fedora and openSUSE systems I had
to install some extra Terminus packages to get the larger sizes as the
installed fonts only went up to 16 points, and I wanted 32. This is the
contents of `/etc/vconsole.conf` on both systems:

```txt
KEYMAP="us"
FONT="ter-v32b"
```
