# Git

- [Beginner guide](#beginner-guides)
- [Undo changes](#undo-changes)

## Beginner guides

- [Git fetch](https://www.atlassian.com/git/tutorials/syncing/git-fetch)
- [Semantic Commit Messages](https://www.conventionalcommits.org/en)

## Undo changes

### Undo changes to a local file

This is for undoing changes on an untracked file.

```bash
git checkout -- <file>
```

There is also the new command `git restore`.

```bash
git restore <file>
```

Type `man git restore` for more about this command, especially the `--staged` and `--worktree ` options.

### Undo a git add

```bash
git reset <file>
```

See [here](https://stackoverflow.com/questions/348170/how-do-i-undo-git-add-before-commit) for more.

### Undo an Unpublished Commit

```bash
git reset HEAD~
```

`git reset` is the command responsible for the **undo**. It will undo your last commit while **leaving your working tree (the state of your files on disk) untouched**. You'll need to add them again before you can commit them again.

More explanations [here](https://stackoverflow.com/a/927386).

### Revert a Git repository to a previous commit

```bash
git revert --no-commit 0d1d7fc3..HEAD # Replace the commit hash by the one you want to rollback to
git commit
```

This will revert everything from the `HEAD` back to the commit hash (excluded), meaning it will recreate that
commit state in the working tree as if every commit after `0d1d7fc3` had been walked back. You can then commit
the current tree, and it will create a brand new commit essentially equivalent to the commit you "reverted" to.

The `--no-commit` flag lets git revert all the commits at once - otherwise you'll be prompted for a message for
each commit in the range, littering your history with unnecessary new commits.

See [this](https://stackoverflow.com/a/21718540) SO answer for detailled explanations.

#### IMPORTANT

Note that this only works if there was no merge commit since the commit we want to rollback to. See
[this answer](https://stackoverflow.com/a/15563149) if merge commits exist.
