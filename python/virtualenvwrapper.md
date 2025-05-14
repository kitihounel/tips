# Virtualenvwrapper Installation Guide

The content of this file describes how to make a **user installation** of `virtualenvwrapper`.

It is heavily based on the tutorial from [MDN](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/development_environment).

I use this as a remainder since I don't want to always check the official documentation when I need to configure a new environment
on a new computer.

Also, I mainly work under Ubuntu. So the process described here is only tested for that distro.

## Install Python 3 and PIP

Python 3 (and PIP) is usually available by default on the system as `python3`. If you want to make it available as `python`, install the package `python-is-python3`.

```bash
sudo apt install python-is-python3
```

## Install Virtualenvwrapper

We will make a **user install** of `virtualenvwrapper`.

```bash
pip3 install --user virtualenvwrapper
```

## Environment Variables Configuration

Add the following lines to the end of your `.bashrc` file. These set the location where the virtual environments should live, the location of your development project directories, the path to your global python executable and the location of the script installed with this package.

```bash
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/src/python
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source $HOME/.local/bin/virtualenvwrapper.sh
```

You will see in the official doc that the last line is different. They use:
```bash
source /usr/local/bin/virtualenvwrapper.sh
```

Remember that we made a **user install**. So the `virtualenvwrapper.sh` is located at `~/.local/bin/virtualenvwrapper.sh` and not at `/usr/local/bin/virtualenvwrapper.sh`.

## Final Step

Reload the `.bashrc` file by running the following command in the terminal:

```bash
source .bashrc # this should be executed from your home directory
```

At this point you should see a bunch of scripts being run as shown below:

```bash
virtualenvwrapper.user_scripts creating /home/ubuntu/.virtualenvs/premkproject
virtualenvwrapper.user_scripts creating /home/ubuntu/.virtualenvs/postmkproject
# ...
virtualenvwrapper.user_scripts creating /home/ubuntu/.virtualenvs/preactivate
virtualenvwrapper.user_scripts creating /home/ubuntu/.virtualenvs/postactivate
virtualenvwrapper.user_scripts creating /home/ubuntu/.virtualenvs/get_env_details
```

You are done. Enjoy using your tool.

## Available Commands

- `mkvirtualenv <name of environment>` - Create a new virtual environment
- `deactivate` - Exit out of the current Python virtual environment
- `workon` - List available virtual environments
- `workon <name of environment>` - Activate the specified Python virtual environment
- `rmvirtualenv <name of environment>` - Remove the specified environment

## Important

If you are having troubles installing the tool, refer to its official doc available [here](https://virtualenvwrapper.readthedocs.io/en/latest/).

You can also take a look at the script `~/.local/bin/virtualenvwrapper.sh`. There is a really good documentation inside it.

## Useful Information about the `dot` and `source` Commands Inside `bash`

`source`, on most systems, is just a more readable alias for the dot command (`.`). Since the IEEE POSIX standards outline 
that the dot command is the only method to source commands in a shell file, using the dot command is the safest option ifportability is a concern. The source and dot commands both execute the script under the same process as the shell it is
executed in, while `./` executes the script under a different process, meaning a new shell is used to run the process, which,
upon completion, is closed. The only difference between the behavior of source and dot is that when using the dot command you
must specify the full path to the file you wish to execute (or have that specific path in your PATH variable), whereas `source`
is not encumbered by this limitation.

More on the topic [here](https://medium.com/@sdbutalla/what-really-is-the-difference-between-the-source-and-dot-commands-in-bash-zshell-736896bc26a3).
