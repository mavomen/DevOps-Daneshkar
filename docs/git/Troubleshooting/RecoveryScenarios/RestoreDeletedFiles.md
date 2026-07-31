---
id: RestoreDeletedFiles
aliases: []
tags: []
---

# Restore Deleted Files

How to restore a deleted file depending on whether deletion was committed.

## Case A: File deleted but not committed yet

```bash
git restore <path/to/file>
```

If deletion was staged:

```bash
git restore --staged <path/to/file>
git restore <path/to/file>
```

## Case B: File deleted in a previous commit

Restore from a commit where it existed:

```bash
git log -- <path/to/file>
git restore --source=<commit-hash> -- <path/to/file>
```

Alternative legacy form:

```bash
git checkout <commit-hash> -- <path/to/file>
```

(See [[git-checkout-file]])

## Related Notes

- [[git-restore]]
- [[git-log]]
- [[git-checkout-file]]
