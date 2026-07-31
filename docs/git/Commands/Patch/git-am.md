---
id: git-am
aliases: []
tags: []
---

# git am

Apply a series of patches from mailbox/email format and create commits from them.

## Syntax

```bash
git am [<options>] <mbox>
git am [<options>] <patch>...
git am --continue | --abort | --skip
```

## Description

`git am` (“apply mailbox”) applies patches that include **commit metadata** (author, date, message), and then creates commits.

This is different from [[git-apply]] which applies changes but does **not** create commits or preserve author metadata.

Typical sources for `git am` patches:

- `git format-patch` output (`*.patch`)
- emailed patches (mbox format)

## Basic Usage

### Apply one patch file

```bash
git am 0001-some-change.patch
```

### Apply multiple patch files

```bash
git am *.patch
```

### Apply an mbox file

```bash
git am changes.mbox
```

## Common Options

### Keep going on patch series

`git am` is designed for patch series; if a conflict occurs, resolve then continue.

## Conflict Handling

### When a patch fails

Git stops and tells you which patch failed.

1. Inspect state:

```bash
git status
```

2. Fix conflicts manually (edit files), then stage:

```bash
git add .
```

3. Continue:

```bash
git am --continue
```

### Skip the current patch

```bash
git am --skip
```

### Abort and return to pre-apply state

```bash
git am --abort
```

## Useful Safety Checks

### Check if patch applies cleanly (without committing)

If you just want to see if it would apply, you can often use:

```bash
git apply --check 0001-some-change.patch
```

(But note: `git apply` doesn’t verify/handle email metadata the same way as `git am`.)

## Common Workflows

### Import changes from another repo via patches

In source repo:

```bash
git format-patch -n <base>..HEAD
# produces 0001-*.patch, 0002-*.patch ...
```

In target repo:

```bash
git am /path/to/patches/*.patch
```

## Troubleshooting

### “Patch format detection failed”

- ensure the patch is in email/mailbox format (from `git format-patch`)
- if it’s a plain diff, use [[git-apply]] instead

### “Applying: …” but conflicts appear

This is normal if the patch doesn’t match current code. Resolve and `--continue`.

## Related Commands

- [[git-apply]] - apply patch without creating commits
- [[git-format-patch]] - generate email patches (optional future note)
- [[git-rebase]] - alternative way to transplant commits (different purpose)
- [[git-cherry-pick]] - apply commits directly if you have repo access
