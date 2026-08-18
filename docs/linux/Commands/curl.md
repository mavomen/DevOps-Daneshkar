---
id: curl
aliases: []
tags: []
---

# curl

Transfer data from/to URLs.

## Syntax

```bash
curl [options] [URL]
```

## Common Usage

```bash
curl https://example.com
```

```bash
curl -I https://example.com
```

```bash
curl -o file.zip URL
```

```bash
curl -X POST -d 'data' URL
```

## Tips

- -I for headers only, -o for output file, -X for method, -L to follow redirects

## Related Notes

- [[NetworkingBasics]]
