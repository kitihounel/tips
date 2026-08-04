# Bash scripting notes

- [About variables](#about-variables)
- [The case statement](#the-case-statement)
- [String manipulation](#string-manipulation)
- [Loops](#loops)

# About variables

Most of the time, variables used in scripts are strings, even when they don't look like it.

Consider this sample:

```bash
K=$(wc -l /path/to/some/file)
if [[ $K -eq 0 ]] ; then
    echo 'Some dumb message'
if
```

The literal `0` is a string, so is the value of `$K`. It is as if in conditions,
Bash uses variables are placeholders, blindly replace them with their content, and
passes the resulting expression to the `test` command.

So, something like this won't work:

```bash
SOME_VAR='A string with spaces'
if [[ $SOME_VAR == 'Another string' ]] ; then
    echo 'A useful message'
if
```

So, make use of quotes as much as possible to avoid problems.

## The case statement

### Syntax

```bash
case expression in
   pattern1) execute commands;;
   pattern2) execute commands;;
   pattern3) execute commands;;
   pattern4) execute commands;;
   * )       execute some default commands or nothing ;;
esac
```

### Example

```bash
echo 'Do you want to destroy your entire file system?'
read ANSWER

case "$ANSWER" in
    yes  ) echo 'I hope you know what you are doing!' ;;
    "no" ) echo 'You have some common sense!' ;;
    y | Y | YES )
        echo 'I hope you know what you are doing!'
        echo "I am supposed to type: 'rm -rf /'"
        echo 'But I am not going to let you commit suicide'
        ;;
    "n" | "N" | "NO" )
        echo 'You have some common sense!' ;;
    * )
        echo 'You have to give an answer!' ;;
esac
```

As you can see, you can put space between a patterns and its closing bracket for readability.
And you don't need to put patterns in quotes if they do not contain space.

## String manipulation

### String comparison

| Operator               | Meaning                                                         |
| ---------------------- | --------------------------------------------------------------- |
| `[[ STR1  > STR2 ]]`   | Compares the sorting order of `STR1` and `STR2`                 |
| `[[ STR1 == STR2 ]]`   | Compares the characters in `STR1` with the characters in `STR2` |

Remember, in most cases, we can use single square brackets ( `[ ]` ) instead of double
( `[[ ]]` ) in comparisons and logical tests, but the more modern doubled form helps
avoid some errors, such as those that can arise when doing a comparison with empty strings
and environment variables.

It can also help to always surrond variables with double quotes when doing comparisons. 

### Get the length of a string

```bash
LEN=${#MY_STR}
```

### Slicing

At times, you may not need to compare or use an entire string. To extract
the first `N` characters of a string, we can specify:

```
${STR:0:N}
```
Here, `0` is the offset in the string (i.e., which character to begin from) where
the extraction needs to start, and `N` is the number of characters to be extracted.

To extract all characters in a string after a given character, for example a dot,
use the following expression:

```
${STR#*.}
```

**Examples:**

```bash
$ NAME='Riley E. Freeman'
$ echo ${NAME#*.}   # displays 'Freeman'
$ echo ${NAME#*R}   # displays 'iley E. Freeman'
$ echo ${NAME#*e}   # displays 'y E. Freeman'
$ echo ${NAME#*E}   # displays '. Freeman'
```

## Loops


### For loop

```bash
for variable-name in list
do
    execute one iteration for each item in the list until the list is finished
done
```

### While loop

```bash
while condition is true
do
    Commands for execution
done
```

### Until loop

```bash
until condition is false
do
    Commands for execution
done
```
