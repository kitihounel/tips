# ssh

This document describes how to generate SSH keys and add them to `ssh-agent`.

The content in this file comes from two main sources.
- [Github doc](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [FOSS Linux](https://www.fosslinux.com/122405/how-to-install-and-use-ssh-agent-on-ubuntu.htm)
- [freeCodeCamp](https://www.freecodecamp.org/news/the-ultimate-guide-to-ssh-setting-up-ssh-keys/)

## Main sections

- [Generating a new SSH key](#generating-a-new-ssh-key)
- [Adding your SSH key to the ssh-agent](#adding-your-ssh-key-to-the-ssh-agent)
- [Auto-start SSH agent](#auto-start-ssh-agent)
- [List keys added to ssh-agent](#list-keys-added-to-ssh-agent)
- [Remove all keys from ssh-agent](#remove-all-keys-from-ssh-agent)
- [Manage multiple keys](#manage-multiple-ssh-keys)
- [Useful configuration examples](#useful-configuration-examples)

## Generating a new SSH key

1. Open a terminal.

2. Paste the text below, replacing the email used in the example with your email address.

    ```sh
    ssh-keygen -t ed25519 -C "your.email@example.com"
    ```

    This creates a new SSH key, using the provided email as a label.

    ```
    > Generating public/private ALGORITHM key pair.
    ```

    When you're prompted to "Enter a file in which to save the key", you can press Enter to accept the default file location.
    Please note that if you created SSH keys previously, ssh-keygen may ask you to rewrite another key, in which case we
    recommend creating a custom-named SSH key. To do so, type the default file location and replace `id_ALGORITHM` with your
    custom key name.

    ```
    > Enter a file in which to save the key (/home/YOU/.ssh/ALGORITHM):[Press enter]
    ```

    At the prompt, type a secure passphrase.

    ```
    > Enter passphrase (empty for no passphrase): [Type a passphrase]
    > Enter same passphrase again: [Type passphrase again]
    ```

## Adding your SSH key to the ssh-agent

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated
a new SSH key. 

1. Start the ssh-agent in the background.

  ```sh
  $ eval "$(ssh-agent -s)"
  > Agent pid 5954
  ```

2. Add your SSH private key to the ssh-agent.

    If you created your key with a different name, or if you are adding an existing key that has a different name, replace `id_ed25519` in the command with the name of your private key file.

    ```sh
    ssh-add ~/.ssh/id_ed25519
    ```

## Auto-start ssh-agent

To auto-start ssh-agent whenever you start a terminal, you can add the `eval "$(ssh-agent -s)"` command to your shell's
profile script.

For bash users, the file is `~/.bashrc`. For Zsh users, it is `~/.zshrc`.

```sh
echo 'eval "$(ssh-agent -s)"' >> ~/.bashrc
```

## List keys added to ssh-agent

```sh
ssh-add -l
```

## Remove all keys from ssh-agent

```sh
ssh-add -D
```

## Enter SSH passphrase once

Add the following at the beginning of your `config` file.

```
AddKeysToAgent yes
```

See [here](https://man.openbsd.org/ssh_config.5#AddKeysToAgent) for more details.

## Manage multiple SSH keys

Though it's considered good practice to have only one public-private key pair per device, sometimes you need to use
multiple keys or you have unorthodox key names. For example, you might be using one SSH key pair for working on your
company's internal projects, but you might be using a different key for accessing a client's servers. On top of that,
you might be using a different key pair for accessing your own private server.

The solution is to automate adding keys, store passwords, and to specify which key to use when accessing certain servers.

The first thing we are going to solve using the `config` file is to avoid having to add custom-named SSH keys using `ssh-add`. Assuming your private SSH key is named `~/.ssh/id_ed25519`, add following to the config file:

```
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519 # Make sure to replace this by the name of your private key file
  IdentitiesOnly yes
```

Next, make sure that `~/.ssh/id_ed25519` is not in ssh-agent by opening another terminal and running the following command:

```sh
ssh-add -D
```

Now if you try cloning a GitHub repository, your config file will use the key at `~/.ssh/id_ed25519`.

## Useful Configuration Examples

```
Host bitbucket-corporate
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/id_ed25519_corp
  IdentitiesOnly yes
```

Now you can use `git clone git@bitbucket-corporate:COMPANY/project.git`.

```
Host bitbucket-personal
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/id_ed25519_personal
  IdentitiesOnly yes
```

Now you can use `git clone git@bitbucket-personal:USERNAME/other-pi-project.git`.

```
Host myserver
  HostName ssh.username.com
  Port 1111
  IdentityFile ~/.ssh/id_ed25519_personal
  IdentitiesOnly yes
  User username
  IdentitiesOnly yes
```

Now you can SSH into your server using `ssh myserver`. You no longer need to enter a port and username every time
you SSH into your private server.

**IMPORTANT**

For more information about the content the SSH `config` file, see [here](https://www.ssh.com/academy/ssh/config).
