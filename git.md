# Git

- [Beginner guide](#beginner-guides)
- [Undo changes](#undo-changes)

## Beginner guides

- [Git fetch](https://www.atlassian.com/git/tutorials/syncing/git-fetch)
- [Semantic Commit Messages](https://www.conventionalcommits.org/en)

## Undo changes

### Undo changes to a local file

This is for undoing changes on an untracked file.

```
git checkout -- <file>
```

There is also the new command `git restore`.

```
git restore <file>
```

Type `man git restore` for more about this command, especially the `--staged` and `--worktree ` options.

### Undo a git add

```
git reset <file>
```

See [here](https://stackoverflow.com/questions/348170/how-do-i-undo-git-add-before-commit) for more.

### Revert a Git repository to a previous commit

See [this](https://stackoverflow.com/a/21718540) SO answer for detailled explanations.

Note that this only works if there was no merge commit since the commit we want to rollback to. See
[this answer](https://stackoverflow.com/a/15563149) if merge commits exist.
