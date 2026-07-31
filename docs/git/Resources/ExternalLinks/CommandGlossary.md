---
id: CommandGlossary
aliases: []
tags: []
---

# Command Glossary

Quick “what does it do?” reference for major commands in this vault.

## Daily core

| Command      | Purpose                           | Note           |
| ------------ | --------------------------------- | -------------- |
| `git status` | show working tree + staging state | [[git-status]] |
| `git add`    | stage changes                     | [[git-add]]    |
| `git commit` | create a commit                   | [[git-commit]] |
| `git diff`   | view changes                      | [[git-diff]]   |
| `git log`    | view history                      | [[git-log]]    |
| `git show`   | inspect commit/object             | [[git-show]]   |

## Branching / integration

| Command           | Purpose                     | Note                |
| ----------------- | --------------------------- | ------------------- |
| `git branch`      | list/create/delete branches | [[git-branch]]      |
| `git switch`      | switch branches             | [[git-switch]]      |
| `git merge`       | integrate history           | [[git-merge]]       |
| `git rebase`      | reapply commits on new base | [[git-rebase]]      |
| `git cherry-pick` | apply selected commit(s)    | [[git-cherry-pick]] |

## Remotes

| Command      | Purpose                                | Note           |
| ------------ | -------------------------------------- | -------------- |
| `git remote` | manage remotes                         | [[git-remote]] |
| `git fetch`  | download + update remote-tracking refs | [[git-fetch]]  |
| `git pull`   | fetch + integrate                      | [[git-pull]]   |
| `git push`   | publish commits/refs                   | [[git-push]]   |

## Undo / cleanup

| Command                        | Purpose                               | Note                  |
| ------------------------------ | ------------------------------------- | --------------------- |
| `git restore`                  | restore files from a source           | [[git-restore]]       |
| `git reset`                    | move refs / unstage / (maybe) discard | [[git-reset]]         |
| `git revert`                   | undo via a new commit                 | [[git-revert]]        |
| `git clean`                    | remove untracked files/dirs           | [[git-clean]]         |
| `git checkout <ref> -- <path>` | legacy “restore file” form            | [[git-checkout-file]] |

## Inspection / recovery

| Command      | Purpose                     | Note           |
| ------------ | --------------------------- | -------------- |
| `git blame`  | line attribution            | [[git-blame]]  |
| `git reflog` | ref movement history        | [[git-reflog]] |
| `git bisect` | find bug-introducing commit | [[git-bisect]] |

## Advanced operations

| Command             | Purpose                          | Note                  |
| ------------------- | -------------------------------- | --------------------- |
| `git stash`         | park working changes temporarily | [[git-stash]]         |
| `git tag`           | create/list tags                 | [[git-tag]]           |
| `git worktree`      | multiple working dirs            | [[git-worktree]]      |
| `git submodule`     | nested repos pinned to commits   | [[git-submodule]]     |
| `git filter-branch` | rewrite history by filtering     | [[git-filter-branch]] |

## Plumbing

| Command           | Purpose                       | Note                |
| ----------------- | ----------------------------- | ------------------- |
| `git cat-file`    | inspect object contents/types | [[git-cat-file]]    |
| `git hash-object` | hash/write object content     | [[git-hash-object]] |
| `git write-tree`  | write tree from index         | [[git-write-tree]]  |
| `git commit-tree` | create commit from tree       | [[git-commit-tree]] |
| `git update-ref`  | move refs directly            | [[git-update-ref]]  |
| `git rev-parse`   | resolve refs to hashes        | [[git-rev-parse]]   |
