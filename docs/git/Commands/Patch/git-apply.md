---
id: git-apply
aliases: []
tags: []
---

# git apply

Apply a patch to your working directory (and optionally the index).

## Syntax

```bash
git apply [<options>] <patch>...
git apply [<options>] --stdin
```

## Description

`git apply` takes a unified diff (patch) and applies it:

- to the working directory by default
- optionally also to the index (staging area)

It does **not** create commits.

If your patch is an email-style patch produced by `git format-patch` and you want author/metadata preserved, consider `git am` instead.

Related:

- [[git-commit]]
- [[StagingArea]]
- [[git-am]] (optional future note)

## Common Usage

### Apply a patch file to working directory

```bash
git apply fix.patch
```

### Dry-run / check if it would apply cleanly

```bash
git apply --check fix.patch
```

### See what it would change (summary/stat)

```bash
git apply --stat fix.patch
```

### Apply and stage the result (update index)

```bash
git apply --index fix.patch
```

### Apply only to the index (no working tree)

```bash
git apply --cached fix.patch
```

### Apply from stdin

```bash
curl -L https://example.com/fix.patch | git apply
```

## Conflict-ish Handling

### Create `.rej` rejects instead of failing hard

```bash
git apply --reject fix.patch
```

### Try a 3-way fallback (if possible)

```bash
git apply -3 fix.patch
```

> `-3` works best when the patch includes enough context and Git can find a suitable base.

## Other Useful Options

### Reverse a patch (undo it)

```bash
git apply -R fix.patch
```

### Whitespace handling

```bash
git apply --whitespace=fix fix.patch
git apply --whitespace=warn fix.patch
git apply --whitespace=nowarn fix.patch
```

## Troubleshooting

### “patch failed” / “does not apply”

- confirm you’re on the correct base commit/branch
- run `git apply --check` to verify applicability
- try `git apply -3`
- if patch paths are off, you may need to adjust prefixes when generating the patch (or edit the patch)

## Related Notes

- [[git-diff]]
- [[git-apply]]
- [[git-commit]]
- [[StagingArea]]
- [[Troubleshooting/CommonProblems/MergeConflicts|Merge Conflicts]]
