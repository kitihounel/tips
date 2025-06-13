# Markdown

## Link Syntax

You can create an inline link by wrapping link text in brackets `[ ]`, and then wrapping the URL in parentheses `( )`.

## Link to part of the same document

You create one with `[link text](#my-multi-word-header)`.

## Comments in markdown

The recommended syntax is:

```txt
[//]: # (This may be the most platform independent comment)
```

There are other alternatives:

```txt
[comment]: <> (This is a comment, it will not be included)
[comment]: <> (in  the output file unless you use it in)
[comment]: <> (a reference style link.)
```
 Or:

 ```txt
 [//]: <> (This is also a comment.)
 ```

 For maximum portability it is important to insert a blank line before and after this type of comments, because some
 Markdown parsers do not work correctly when definitions brush up against regular text.

**Source:** [SO](https://stackoverflow.com/a/20885980).
