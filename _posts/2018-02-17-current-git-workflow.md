---
layout: post
title: "Current Git workflow"
date: "2018-02-17 12:00:00 -0200"
author: "Lemuel Roberto"
meta: "git"
---

## Summary

1. Create a branch from master (or whaterver is needed)
2. Sync branch with master and resolve conflicts when needed
3. Commit often and as soon as possible when developing a feature or fixing a bug
4. Smalls and atomic commits that changes code base as little as possible
5. Rebase to group commits and reorder in a meaningful way
6. Write commit's message for my future self and others to understand it's context
7. Improve code after code review
8. Commit & rebase to maintain a meaningful and readable Git history until pass code review
9. Merge to master branch

## 1. Create a branch from master

A branch here is nothing more than a safe workspace for you to work on.
You can write code, test things and commit as much as you can without messing up the mainline code base.

## 2. Sync branch with master and resolve conflicts when needed

To avoid lots of conflicts on merge, sync your workspace branch with master branch when needed. Tip: you can check if there is new commits on branch just using `git fetch` from time to time.

Use `git rebase` to sync your branch and maintain a more readble git history. See [Rewriting history](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase) to understand more.

## 3. Commit often and as soon as possible when developing a feature or fixing a bug

As you get more comfortable with `git reset`, `git rebase` and `git reflog`, you'll notice that it's not a big deal to commit your tries & errors to save an idea or work in progress code and than rewrite Git history.

## 4. Smalls and atomic commits that changes code base as little as possible

Small changes to the code base are easy to pick to use in another branch, to rewrite or group with a bigger code change if it makes sense or even to delete if needed.

## 5. Rebase to group commits and reorder in a meaningful way

Sometimes there are so many commits in a random order that is impossible to follow a repository change's history.

Once you're sure of your solution or even a small part of the solution, use `git rebase` and it's commands to create a better Git history for your feature or bugfix.

## 6. Write commit's message for my future self and others to understand it's context

You can write a really easy-to-understand code with good documentation, but sometimes you also want to know the motive for that change or feature.

In your commit message, explain the motives of the code changes and reference the origin issue on a project management system like JIRA or GitHub issues for further info. See a [good commit message](https://github.com/torvalds/subsurface-for-dirk/commit/b6590150d68df528efd40c889ba6eea476b39873) from Linus Torvalds.

## 7. Improve code after code review

Improve code quality from the feedback of other developers and QA testers.

## 8. Commit & rebase to maintain a meaningful and readable Git history until pass code review

When improving your code base, make sure you're always maintaining a readable Git history.

## 9. Merge to master branch

Finish your team process of tests, integrations or whatever you do and merge your code changes back to master.


## 10. Best tip EVER

Keep trying to find better workflows for you and your team ;)
