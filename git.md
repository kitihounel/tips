# Git

- [Beginner guide](#beginner-guides)
- [Undo changes](#undo-changes)
- [Push only specific commits](#push-only-specific-commits)
- [Copy file from another commit or branch](#copy-file-from-another-commit-or-branch)
- [Fetch a remote branch](#fetch-a-remote-branch)
- [Reset a branch based on another](#reset-a-branch-based-on-another)
- [Using the stash](#using-the-stash)
- [Search in commit messages](#search-in-commit-messages)

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

## Copy file from another commit or branch

There are two options to perform this: using `git checkout` or `git restore`.

**Source:** [StackOverflow](https://stackoverflow.com/questions/307579).

### Using git restore

```sh
git restore --source otherbranch path/to/myfile.txt
```

The difference with `git checkout` (see below) is that `git checkout` copies the file to the working directory
(your files on disk) but also to the staging area (much like a `git add`). `git checkout` by default changes
only the working directory.

### Using git checkout

Run this from the branch where you want the file to end up:

```sh
git checkout otherbranch myfile.txt
```

General formulas:

```txt
git checkout <commit_hash> <relative_path_to_file_or_dir>
git checkout <remote_name>/<branch_name> <file_or_dir>
```

Some notes (from comments in the SO thread):

- Using the commit hash, you can pull files from any commit.
- This works for files and directories.
- Overwrites the file `myfile.txt` and `mydir`.
- Wildcards don't work, but relative paths do.
- Multiple paths can be specified.

## Fetch a remote branch

If you need to fetch a remote branch that is not in your local repository,
use `git switch`.

```bash
git switch name-of-remote-branch
```

You will get an output similar to this:

```txt
branch 'foo-bar-branch' set up to track 'origin/foo-bar-branch'.
Switched to a new branch 'foo-bar-branch'
```

## Reset a branch based on another

To reset a branch named `my-feature-branch` based on the `main` branch for example:

```sh
git switch main && git pull   # get the latest changes from remote
git switch my-feature-branch  # switch back to the feature branch
git reset --hard main
```

## Using the stash

A simple and concise tutorial is available [here](https://www.devroom.io/2008/04/23/git-using-the-stash).

The following sections are taken from the article.

### What is the stash

Git features the stash, which is as much as a good place to store uncommitted changes. When you stash you changes,
they will be stored, and your working copy will be reverted to HEAD (the last commit revision) of your code.

When you restore your stash, you changes are reapplied and you continue working on your code.

### Stash your current changes

```txt
$ git stash save <optional message for later reference>
```

**Example**

```bash
git stash save 'a dummy stash operation'
```

You will get an output like:

```txt
Saved working directory and index state On main: a dummy stash operation
```

### List current stashes

It is possible to have more than one stash. The stash works like a stack. Every time a new stash is saved,
it's put on top of the stack.

```txt
git stash list
stash@{0}: On main: a dummy stash operation
```

The `stash@{0}` is the stash ID, it will be used to restore it later.

The stash ID changes with every stash made. `stash@{0}` refers to the last stash made.

### Apply a stash

```bash
git stash apply stash@{0}
```

You may notice the stash is still there after you have applied it. You can drop it if you don't need it any more.

```bash
git stash drop stash@{0}
```

### Apply and remove the last stash saved

```bash
git stash pop
```

### Wipe all the stashes away

```bash
git stash clear
```

### Search in commit messages

If you need to search for a commit which messages contains a given text, use:

```bash
git log --grep='pattern'
```

**Note:** This will only search in the history of the active branch.
