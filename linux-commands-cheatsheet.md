# Linux Commands Cheat Sheet

Commands I've used so far, grouped by what I'm trying to do. Examples come from [OverTheWire Bandit](bandit-writeup.md).

## Connect
| Command | What it does |
|---|---|
| `ssh <user>@<host> -p <port>` | Log into a remote machine on a given port |

## Move around and look
| Command | What it does |
|---|---|
| `cd <dir>` | Move into a directory |
| `ls` | List files |
| `ls -a` | List files including hidden ones (names starting with `.`) |

## Read a file
| Command | What it does |
|---|---|
| `cat <file>` | Print a file's contents |
| `file <file>` | Show the file type (ASCII text, data, executable) |
| `strings <file>` | Print only the human-readable text inside a file |

## Tricky filenames
| Situation | Fix |
|---|---|
| Name is `-` or starts with `-` | Start the path with `./`, for example `cat ./-` |
| Name has spaces | Quote it, or put `\` before each space |
| Many files at once | `*` is a wildcard. `./*` is the safe form |

## Find files
| Command | What it does |
|---|---|
| `find <where> <tests>` | Search for files |
| `-type f` | Files only |
| `-size 33c` | Exact size (`c` = bytes) |
| `-user <name>`, `-group <name>` | Filter by owner and group |
| `2>/dev/null` | Hide error messages such as "Permission denied". It doesn't grant access |

## Search and filter text
| Command | What it does |
|---|---|
| `grep <word> <file>` | Show lines containing a word or pattern |
| `sort <file>` | Order lines alphabetically |
| `uniq -u` | Show only lines that appear once (sort first) |
| `uniq -c` | Count repeated lines (sort first) |

## Combine commands
| Symbol | What it does |
|---|---|
| <code>&#124;</code> (pipe) | Send one command's output into the next |

```bash
sort data.txt | uniq -u
strings data.txt | grep "=="
```

## Decode
| Command | What it does |
|---|---|
| `base64 -d <file>` | Decode base64 data |

## If the terminal gets messed up
| Command | What it does |
|---|---|
| `reset` | Restore the terminal |
