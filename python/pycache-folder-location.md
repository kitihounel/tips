# pycache settings

- [pycache folder location](#pycache-folder-location)

## pycache folder location

If you don't like having `__pycache__` folders everywhere in your projects, there is simple setting (starting from Python 3.8)
to keep them in a specific location.

Just create an environment variable named `PYTHONPYCACHEPREFIX` (in your `.bashrc` or `.profile`) and set its value the folder
where you want to keep these annoying folders. For example:

```bash
PYTHONPYCACHEPREFIX=$HOME/.pycache-store
```

See [here](https://docs.python.org/3/using/cmdline.html#envvar-PYTHONPYCACHEPREFIX) for the official doc.
