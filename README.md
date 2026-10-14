# OverTheWire Bandit Write-ups

My notes and write-ups from [OverTheWire Bandit](https://overthewire.org/wargames/bandit/), a free wargame that teaches Linux command-line basics and SSH.

> No passwords or credentials are included in this repository, in line with OverTheWire's rules for write-up authors.

## Why I'm doing this
I'm rebuilding hands-on skills for a career in security (SOC and OT/ICS). Writing each level up in my own words helps me remember the commands and explain them.

## Progress
Level names follow the OverTheWire site ("0 → 1" is the task that gets you the password for level 1).

| Level | Goal | Key commands | What I learned |
|---|---|---|---|
| 0 | Log in with SSH on port 2220 | `ssh` | Connecting to a remote server |
| 0 → 1 | Read a file called `readme` | `ls`, `cat` | Reading files |
| 1 → 2 | The file is named `-` | `cat ./-` | A lone dash means standard input, so use a path |
| 2 → 3 | The filename has spaces and starts with `--` | `cat ./--spaces\ in\ this\ filename--` | Escaping spaces, and `./` for dashes |
| 3 → 4 | Find a hidden file | `cd`, `ls -a`, `cat` | Hidden files start with a dot |
| 4 → 5 | Find the only human-readable file | `file ./*`, `cat` | `file` shows a file's type, and `./*` is the safe wildcard when names start with `-` |
| 5 → 6 | Find a file that is readable, 1033 bytes and not executable | `find -size 1033c`, `cat` | `find` can filter by size, and `c` means bytes |
| 6 → 7 | Find a file by owner, group and size anywhere on the server | `find / -type f -user -group -size 2>/dev/null` | Combining `find` filters, and `2>/dev/null` hides errors without granting access |
| 7 → 8 | Find the line next to the word `millionth` | `grep` | Searching inside a file for a word |
| 8 → 9 | Find the only line that appears once | `sort`, `uniq -u` | `uniq` only compares neighbouring lines, so sort first |
| 9 → 10 | Find a readable string preceded by `=` characters | `strings`, `grep` | `strings` pulls readable text out of binary data, and a pipe chains commands |
| 10 → 11 | Decode base64 data | `base64 -d` | Base64 is an encoding, not encryption |
| 11 → 12 | Decode ROT13 text | *(in progress)* | |

## Contents
- [`writeups`](writeups/): one write-up per level
- [`linux-commands-cheatsheet.md`](linux-commands-cheatsheet.md): the commands I've used, in one place

## Credit
All challenges belong to the [OverTheWire](https://overthewire.org) community. This repository contains only my own notes.
