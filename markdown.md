# Markdown

- [Links](#links)
- [Comments](#comments-in-markdown)
- [Tables](#tables)

## Links

### Basics

You can create an inline link by wrapping link text in brackets `[ ]`, and then wrapping the URL in parentheses `( )`.

### Link to part of the same document

You create one with `[link text](#my-multi-word-header)`.

## Comments in markdown

The recommended syntax is:

```markdown
[//]: # (This may be the most platform independent comment)
```

There are other alternatives:

```markdown
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

**Source:** [StackOverflow](https://stackoverflow.com/a/20885980).

## Tables

### Basics

To add a table in Markdown, use the vertical line `|` to separate each column, and use three or more dashes `---`
to create each column's header. A vertical line should also be added at either end of the row.

```markdown
| Month    | Savings |
| -------- | ------- |
| January  | $250    |
| February | $80     |
| March    | $420    |
```

Cell widths can vary, as shown below:

```markdown
| Month | Savings |
| -------- | ------- |
| January | $250 |
| February | $80 |
| March | $420 |
```

The output will look exactly the same.

### Text alignment

Align text in the columns to the left, right, or center by adding a colon `:` to the left, right, or on both side of the dashes
`---` within the header row.

```markdown
| Item              | In Stock | Price |
| :---------------- | :------: | ----: |
| Python Hat        |   True   | 23.99 |
| SQL Hat           |   True   | 23.99 |
| Codecademy Tee    |  False   | 19.99 |
| Codecademy Hoodie |  False   | 42.99 |
```

- `:--` means the column is left aligned.
- `--:` means the column is right aligned.
- `:-:` means the column is center aligned.

### Text formatting

Text can be formatted within tables. For example, links, emphasis, and inline code (words or phrases in backticks only,
not code blocks) are all readily available for use within a table.

Several formatting options are not available within tables, including:

- headings,
- blockquotes,
- horizontal rules,
- images,
- lists,
- HTML tags.

### Escaping Characters

Pipe characters `|` can be displayed in a table with the HTML character code `&#124;`.

**Source:** [CodeCademy](https://www.codecademy.com/resources/docs/markdown/tables).
