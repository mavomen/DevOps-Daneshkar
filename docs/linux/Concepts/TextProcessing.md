---
id: TextProcessing
aliases: []
tags: []
---

# Text Processing

Linux provides powerful tools for text manipulation from the command line.

## Core Tools

| Tool | Purpose | Example |
|------|---------|---------|
| `grep` | Search patterns | `grep -r "error" /var/log/` |
| `sed` | Stream edit | `sed 's/old/new/g' file` |
| `awk` | Field processing | `awk '{print $1}' file` |
| `cut` | Extract columns | `cut -d: -f1 /etc/passwd` |
| `sort` | Sort lines | `sort -u file` |
| `uniq` | Deduplicate | `sort file | uniq -c` |
| `wc` | Count lines/words | `wc -l file` |
| `head` | First N lines | `head -20 file` |
| `tail` | Last N lines | `tail -f /var/log/syslog` |
| `tr` | Translate chars | `tr 'a-z' 'A-Z'` |
| `diff` | Compare files | `diff file1 file2` |
| `tee` | Split output | `command | tee output.log` |
| `xargs` | Build commands | `find . -name "*.tmp" | xargs rm` |

## grep Patterns

```bash
grep "error" logfile                        # Simple match
grep -i "error" logfile                     # Case-insensitive
grep -r "TODO" src/                         # Recursive
grep -n "function" script.py                # With line numbers
grep -c "error" logfile                     # Count matches
grep -v "debug" logfile                     # Invert match
grep -A3 -B1 "error" logfile                # Context lines
grep -E "err|warn|crit" logfile             # Extended regex
```

## sed One-Liners

```bash
sed -i 's/old/new/g' file                   # Replace in-place
sed -n '10,20p' file                        # Print lines 10-20
sed '/^#/d' file                            # Remove comments
sed '2d' file                               # Delete line 2
sed -i '/pattern/d' file                    # Delete matching lines
```

## awk One-Liners

```bash
awk '{print $1, $3}' file                   # Print columns 1 and 3
awk -F: '{print $1}' /etc/passwd            # Custom delimiter
awk '/pattern/ {print}' file                # Filter lines
awk '{sum += $1} END {print sum}' file      # Sum column
awk 'NR==5' file                            # Print line 5
```

## Related Notes

- [[ShellBasics]] — Pipes and redirection
- [[GrepRegexPatterns]] — grep regex patterns
- [[sed]] — sed command
- [[awk]] — awk command
