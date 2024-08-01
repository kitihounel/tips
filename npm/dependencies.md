# Dependencies

These notes are about some usages of `npm list` command.

## Project or Package Dependencies

You can list a project dependencies with the following command (You must be inside the project folder):

```bash
npm ls
```

There is the `--depth` option that can help displaying transitive dependencies. The following command will show the project dependencies and their direct dependencies.

```bash
npm ls --depth=1
```

## Reverse Dependencies

To list the packages used in your project that depend on a given one (named for example `pkg`):

```bash
npm ls pkg
```

## List Globally Installed Packages

```bash
npm ls -g
```

Maybe you want to your globally installed packages that depend on a given one:

```bash
npm ls -g package-name
```
