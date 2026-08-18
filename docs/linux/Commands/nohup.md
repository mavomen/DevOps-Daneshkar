---
id: nohup
aliases: []
tags: []
---

# nohup

Run command immune to hangups.

## Syntax

```bash
nohup command [args]
```

## Common Usage

```bash
nohup ./script.sh &
```

```bash
nohup python app.py > app.log 2>&1 &
```

## Tips

- Output goes to nohup.out by default. Use > to redirect. & runs in background

## Related Notes

- [[ProcessManagement]]
