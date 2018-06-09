---
layout: post
title: "The day I lost the HEAD"
date: "2018-06-09 16:00:00 -0300"
author: "Lemuel Roberto"
meta: "git"
---

## What a lovely saturday morning

I was playing with some code and I was just rebasing a few commits and suddenly all my system went down. I rebooted the OS and went back to work but for my dispair and I checked the current state of my working branch with `git status` and all I got was a git fatal error message: **fatal: missing object**.

I tried out a few things but without help. Looking for some answers on Stack Overflow, almost all of them stated tha the best thing I could do was to restart the repo and lost all unpushed commits to remote. That was not an option not because of the comits, but for the defeated in recovering my work. What if it's was not an option? What could I do?

One [Stack Overflow answer](https://stackoverflow.com/a/4263009/5111444) stated that it was possible reconstruct a tree object and sugest a screencast about git internals. Unfortunately unavailable.

## A path to recover a broken git repository

After a quick web search I got some insights of what I had to do the when I found the [Repairing and recovering broken git repositories](https://git.seveas.net/repairing-and-recovering-broken-git-repositories.html) article.

After a few tries, these are the steps I did to solve my case:
1. replaced the HEAD to a valid tree
2. changed HEAD to the closest valid commit I had
3. saved all changes I've had done and lost in a diff file
4. replaced the broken branch's HEAD reference to the lasted valid commit on remote
5. recovered the lost changes \o/

### Replace the HEAD file

Edit the git HEAD file to point to the closest healthy branch as you can be from the broken one.

`echo 'ref: refs/heads/the-closest-healthy-branch' > .git/HEAD`

### Look for a healthy commit

> Reference logs, or "reflogs", record when the tips of branches and other references were updated in the local repository -- git reflog man page

A git reflog call should output something like this and all you have to do is to choose a change to be the new HEAD.

```
baddfe7 (HEAD -> master, origin/master, origin/HEAD) HEAD@{0}: commit (amend): Add book notes DDIA
e7a4c96 HEAD@{1}: commit: Add book notes
12160d3 HEAD@{2}: rebase -i (finish): returning to refs/heads/master
12160d3 HEAD@{3}: rebase -i (pick): Change footnote description
8d6f101 HEAD@{4}: commit (amend): Add post about encoding in PHP
27dd10b HEAD@{5}: rebase -i: fast-forward
0c59227 HEAD@{6}: rebase -i (start): checkout HEAD~3
ba9390f HEAD@{7}: commit (amend): Change footnote description
1642353 HEAD@{8}: commit: Change footnote description
27dd10b HEAD@{9}: commit: Add post about encoding in PHP

```

For example you could go back to the *12160d3* changes using `git reset 12160d3` ;)

### Save the changes

A simple `git diff origin/the-branch-you-want-to-compare.. > my-changes.diff` is enough to save your changes for future recovery.

### Replace the branch's HEAD

Get the latest commit hash on your remote serve for the broken branch and fix the local branch's HEAD reference.

`echo 'latest-commit-hash' .git/refs/heads/broken-branch`

Now I was already good to work on the branch.

### Apply the lost changes

The final step is to apply the changes we have lost on the system's crash. A `git apply my-changes.diff` may give you the latest changes.

Hope this can be of some help ;)
