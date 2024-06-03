# Git Commands and Aliases

A list of learned git commands and helpful aliases for the CLI

## Git Commands

### Stage Changes (make ready for commit)

You can add all files, a single file, or use a wildcard to add multiple.

Add all changes.

`git add .`

Add a single file.

`git add ./path/to/file`

Add multiple files with a wildcard.

`git add ./src/*.md`

### Commit the Currently Staged Changes

`git commit -m "my commit message"`

### Push Changes to the Remote Repo

If this is the first push after setting up the remote origin.

`git push origin main`

Otherwise, push.

`git push`

### Pull All Changes From the Remote Repo

`git pull`

### Create a New Branch

Creates a new branch, gives it a name, and switches to it.

`git checkout -b branch-name`

### Switch to an Existing Branch

`git checkout branch-name`

### Push Branch Changes to Remote (GitHub)

This will push the branch changes to the remote repo. On GitHub if the new branch doesn't exist, it will be created
on the first push.

`git push origin branch-name`

You can set the upstream on the current branch. This way for later pushes and pulls, you don't have to specify
the origin and branch.

`git push --set-upstream origin branch-name`

### Pull Changes From a Remote Branch

`git pull origin branch-name`

### Squash Commits

Sometimes there are too many commits to a WIP branch or PR, and you want to squash them all into one commit that
describes the overall set of changes. Handy for not annoying project maintainers when submitting a PR. Especially if
you've been using a shortcut like the WIP alias below, so there are multiple duplicate commit messages. Sometimes a
project maintainer will specifically ask you to squash commits.

Copy the first commit hash and paste here. Resets commits but leaves all file changes.

`git reset --soft hash`

Now add all changes and a more meaningful commit message.

`git add . && git commit -m "adds support for blah blah`

Now forcefully push to the remote to overwrite the old commits with the new one.

`git push -f`

## Aliases

Aliases can make work easier by saving a lot of typing and remembering complex commands

- Adds and commits all changes. Useful while working on a WIP branch.

`wip='git add . && git commit -m '\"Work in progress\"'`

- Performs a full reset and gives a clean start at the last commit.

`nope='git reset --hard && git clean -f -d && git checkout HEAD'`
