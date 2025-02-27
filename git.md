# Git

- [Beginner guide](#beginner-guides)
- [Undo changes](#undo-changes)
- [Push only specific commits](#push-only-specific-commits)

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

Type `man git restore` for more about this command, especially the `--staged`
and `--worktree ` options.

### Undo a git add

```bash
git reset <file>
```

See [here](https://stackoverflow.com/questions/348170/how-do-i-undo-git-add-before-commit)
for more.

### Undo an Unpublished Commit

```bash
git reset HEAD~
```

`git reset` is the command responsible for the **undo**. It will undo your
last commit while **leaving your working tree (the state of your files on disk) untouched**.
You'll need to add them again before you can commit them again.

More explanations [here](https://stackoverflow.com/a/927386).

### Hard reset

This will destroy any local modifications. **Don't do it if you have uncommitted work you want to keep**.

```bash
git reset --hard 0d1d7fc3 # Replace the commit hash by the one you want to rollback to
```

Alternatively, if there's work to keep:

```bash
git stash
git reset --hard 0d1d7fc3 # Replace the commit hash by the one you want to rollback to
git stash pop
```

This saves the modifications, then reapplies that patch after resetting. You could get merge conflicts,
if you've modified things which were changed since the commit you reset to.

Source: [SO](https://stackoverflow.com/a/4114122).

### Revert a Git repository to a previous commit

```bash
git revert --no-commit 0d1d7fc3..HEAD # Replace the commit hash by the one you want to rollback to
git commit
```

This will revert everything from the `HEAD` back to the commit hash (excluded),
meaning it will recreate that commit state in the working tree as if every
commit after `0d1d7fc3` had been walked back. You can then commit the current
tree, and it will create a brand new commit essentially equivalent to the
commit you "reverted" to.

The `--no-commit` flag lets git revert all the commits at once - otherwise
you'll be prompted for a message for each commit in the range, littering your
history with unnecessary new commits.

See [this](https://stackoverflow.com/a/21718540) SO answer for detailled
explanations.

#### IMPORTANT

Note that this only works if there was no merge commit since the commit we
want to rollback to. See [this answer](https://stackoverflow.com/a/15563149)
if merge commits exist.

## Push only specific commits

Sometimes there are a few commits pending to be pushed but you don't want to
push all of them for some reason, e.g. partial deployment, and so you want
to push them only up to a certain commit.

Then you can do this:

```bash
git push <remote> <commit hash>:<branch>
```

For example, you have 5 commits A > B > C > D > E pending (for simplicity,
ABCDE are commit hashes), and you want to push up to commit "C". The following
will then push A, B, and C to origin/main.

```bash
git push origin C:main
```

### Sources

- https://coderwall.com/p/hexinq/git-push-up-to-a-certain-commit
- https://stackoverflow.com/questions/3230074
