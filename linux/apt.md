# apt

- [Search for packages](#search-for-packages)
- [List installed packages](#list-installed-packages)
- [Check package version](#check-package-version)

## Search for packages

```sh
apt-cache search <search term>  # Output more suitable for scripts and tools like grep
apt search <search term>        # Fancy output with colors
```

## List installed packages

```sh
apt list --installed
```

Source: https://askubuntu.com/questions/17823/how-to-list-all-installed-packages

## Check package version

```sh
apt-cache policy <package name> # or
apt policy <package name>
```
