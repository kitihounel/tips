# Unlocking Ubuntu with a pin

First:

```sh
sudo apt install -y libpam-pwdfile
```

If you don't have the `mkpasswd` command, then you need to install `whois` first:

```sh
sudo apt install whois
```

Then take the username you use to log in, let's say "ben" and do this:

```sh
sudo -i # Make sure you understand what this line does.
cp /etc/pam.d/gdm-password /etc/pam.d/gdm-password.original
echo "ben:$(mkpasswd -5)" > /etc/custompinfile
chmod 400 /etc/custompinfile
```

Then you need to edit `/etc/pam.d/gdm-password` (or other desktop manager or whatever, who cares,
you'll figure it out, the thing that manages your logins, mine is `gdm-password`) and add this line
near the top. The top of my `/etc/pam.d/gdm-password` looks like this. Note that the fields in each
line are delimited by tabs.

```
#%PAM-1.0
auth    sufficient  pam_pwdfile.so pwdfile=/etc/custompinfile
```

Use whatever, gedit, nano, vim, but you need sudo privileges to edit it.

Then I saved te file, quit, and logged out. When I logged back in it only required the pin on the lock screen,
but it didn't accept the pin when asking for sudo privileges, which is what we wanted, otherwise we would have
simply set the password to 1234.

If you mess everything up, you can boot in recovery mode (if you don't have a dual boot with Windows, I think
it is something like pressing **Shift** while it's starting up). Then there will be a menu to choose recovery mode;
in recovery mode you can simply access the shell as root and revert the `/etc/pam.d/gdm-password` back to it's original
state, if you remember it :wink:. That's why it's maybe a good idea to make a backup of the original gdm-password file
like `cp /etc/pam.d/gdm-password /etc/pam.d/gdm-password.original`.

Remember, the `/etc/custompinfile` can be called anything, but the contents inside need to be in this format:
`user:hashedpassword`. And the hashed password is obtained using `mkpasswd -5` when you install the `whois` package and
run it.

Source: [AskUbuntu](https://askubuntu.com/a/1304887).
