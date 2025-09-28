# Password generation

- [OpenSSL](#openssl)
- [pwgen](#pwgen)

## OpenSSL

OpenSSL should be available by default on your Linux distro.

```sh
openssl rand -base64 16 # password in base 64  
openssl rand -hex 24    # password in hex
```

The arguments `16` and `24` are the number of bytes generated, not the number of characters.
For more information, `man openssl-rand`.

## pwgen

You need to install it before using it.

```sh
sudo apt install pwgen
```

Then you can generate a password with:

```sh
pwgen -sy 24 1 # Generate one password with 24 characters
```

The `-s` option forces the command to generate random passwords, while the `-y` option includes
at least one special in the password.
