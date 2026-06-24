# Switch between Java versions

- [Linux](#linux)
- [Ubuntu-specific](#ubuntu-specific)

## Linux

To switch between installed Java versions on Linux, use the `sudo update-alternatives --config java` command.
This tool lets you manage multiple system-wide installations through an interactive menu.

### Step 1: switch the Java runtime

```sh
sudo update-alternatives --config java
```

You will see an output listing your installed versions:

```txt
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
-------------------------------------------------------------------------------------
* 0            /usr/lib/jvm/java-21-openjdk-amd64/bin/java      2111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-17-openjdk-amd64/bin/java      1711      manual mode
  3            /usr/lib/jvm/java-21-openjdk-amd64/bin/java      2111      manual mode

Press <enter> to keep the current choice[*], or type selection number: 

```

Type the selection number (e.g., 2 for Java 17) and press **Enter**.

### Step 2: switch the Java compiler

```sh
sudo update-alternatives --config javac
```

Choose the matching number corresponding to the same Java version you selected in Step 1.

### Step 3 (optional): update other tools

There are other Java-related commands that you can also update, like `javap` and `javadoc` depending on your needs.

### Step 4: update the JAVA_HOME variable

Many build tools like Maven or Gradle rely explicitly on the `$JAVA_HOME` environment variable
rather than the default terminal commands.

If you don't have this variable available on your system, you can skip this part.

1.  Dynamic update for your current profile session:

    ```sh
    export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))
    ```

2.  Permanent fix: Append that line to your environment configuration file (e.g., `~/.bashrc` or `~/.zshrc`)
    so it preserves settings across terminal sessions.

## Ubuntu specific

To switch between installed java versions, use the `update-java-alternatives` command.

- List all Java versions:

    ```sh
    update-java-alternatives --list
    ```

- Set Java version as default (needs root permissions):

    ```sh
    sudo update-java-alternatives --set /path/to/java/version
    ```

- If you have the `JAVA_HOME` set, make sure it points to the correct version.
