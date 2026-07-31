# sed

- [Introduction](#introduction)
- [Command syntax](#command-syntax)
- [Tips](#tips)

## Introduction

Most of the information in this file come from the **Introduction to Linux** course of the Linux Foundation.

`sed` is a powerful text processing tool and is one of the oldest, earliest
and most popular UNIX utilities. It is used to modify the contents of a file
or input stream, usually placing the contents into a new file or output stream.
Its name is an abbreviation for *stream editor*.

`sed` can filter text, as well as perform substitutions in data streams.

Data from an input source / file (or stream) is taken and moved to a working space.
The entire list of operations / modifications is applied over the data in the working
space and the final contents are moved to the standard output space (or stream).

## Command syntax

You can invoke `sed` using commands like those listed in the accompanying table.

| Command                                 | Usage                                                                       |
| --------------------------------------- | --------------------------------------------------------------------------- |
| `sed -e command <filename>`             | Specify editing commands at the command line                                |
| `sed -f scriptfile <filename>`          | Specify a `sed` script, operate on file, and put result on standard out   |
| `echo "I hate you" \| sed s/hate/love/` | Use `sed` to filter standard input, putting output on standard out        |

The `-e` option allows you to specify multiple editing commands simultaneously at
the command line. It is unnecessary if you only have one operation invoked.

## sed basic operations

The table explains some basic operations, where `pattern` is the current string
and `replace_string` is the new string.

| Command                                  | Usage                                                  |
| ---------------------------------------- | ------------------------------------------------------ |
| `sed s/pattern/replace_string/ file`     | Substitute first string occurrence in every line       |
| `sed s/pattern/replace_string/g file`    | Substitute all string occurrences in every line        |
| `sed 1,3s/pattern/replace_string/g file` | Substitute all string occurrences in a range of lines  |
| `sed -i s/pattern/replace_string/g file` | Save changes for string substitution in the same file  |

You must use the `-i` option with care, because the action is not reversible.
It is always safer to use sed without the `–i` option and then replace the file
yourself, as shown in the following example:

```bash
$ sed s/pattern/replace_string/g file1 > file2
```

**Example:** To convert 01/02/... to JAN/FEB/...

```bash
$ sed -e 's/01/JAN/' \
      -e 's/02/FEB/' \
      -e 's/03/MAR/' \
      -e 's/04/APR/' \
      -e 's/05/MAY/' \
      -e 's/06/JUN/' \
      -e 's/07/JUL/' \
     -e 's/08/AUG/' \
      -e 's/09/SEP/' \
      -e 's/10/OCT/' \
      -e 's/11/NOV/' \
      -e 's/12/DEC/'
```

## Tips

By default, `sed` performs substring replacement. Sometimes, you want to replace
whole words, not substrings. To replace a whole word using `sed`, wrap your target
word in word boundary markers so that partial matches are ignored.

The syntax described here is that of the GNU version of `sed`.

```bash
$ sed 's/\bcat\b/dog/g' filename.txt
```

Alternatively, you can use `\<` and `\>`:

```bash
sed 's/\<cat\>/dog/g' filename.txt
```

**Source:** Gemini.
