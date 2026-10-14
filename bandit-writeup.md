# OverTheWire Bandit Write-up

Notes and solutions for the [Bandit wargame](https://overthewire.org/wargames/bandit/), which teaches Linux command-line basics over SSH.

**Progress:** Levels 0 to 11 complete. Level 11 → 12 in progress.

Level names follow the OverTheWire site: "0 → 1" is the task that gets you the password for Level 1. Passwords are intentionally left out.

## Connecting

Every level is an SSH login.

```bash
ssh [username]@[destination] -p [port]
```

- Host: `bandit.labs.overthewire.org`
- Port: `2220`
- Username: `bandit<level>` (for example `bandit1` for Level 1)
- Password: the one found in the previous level

---

## Level 0
**Goal:** log into the game over SSH as `bandit0`. The password is given on the level page.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

## Level 0 → 1
**Goal:** the password is in a file called `readme` in the home directory.

- `ls` lists files in the current directory.
- `cat` prints a file's contents.

```bash
ls
cat readme
```

## Level 1 → 2
**Goal:** the password is in a file called `-`.

A lone `-` means standard input, so `cat -` waits for typing instead of reading a file. Prefix the name with `./` to make it a path.

```bash
cat ./-
```

## Level 2 → 3
**Goal:** the password is in a file called `--spaces in this filename--`.

Two problems here. Spaces split a filename into separate arguments, and a name starting with `--` looks like an option. Starting the path with `./` fixes the second, and escaping the spaces or using quotes fixes the first.

```bash
cat ./--spaces\ in\ this\ filename--
cat "./--spaces in this filename--"
```

## Level 3 → 4
**Goal:** the password is in a hidden file in the `inhere` directory.

- `cd` moves into a directory.
- `ls -a` includes hidden files (names starting with `.`).

```bash
cd inhere
ls -a
cat ...Hiding-From-You
```

## Level 4 → 5
**Goal:** the password is in the only human-readable file in `inhere`.

- `file` shows a file's type (ASCII text, data, executable).
- `*` is a wildcard that matches many filenames. Use `./*` because the filenames start with `-`.

```bash
file ./*
cat ./<filename>
```

## Level 5 → 6
**Goal:** a file under `inhere` that is human-readable, 1033 bytes, and not executable.

`find` searches for files. `-size 1033c` matches an exact size (`c` means bytes).

```bash
find -size 1033c
cat ./maybehere07/.file2
```

## Level 6 → 7
**Goal:** a file anywhere on the server, owned by user `bandit7` and group `bandit6`, 33 bytes.

- `-type f`: files only
- `-user` and `-group`: filter by owner and group
- `-size 33c`: exact size in bytes
- `2>/dev/null`: hide error messages such as "Permission denied". It does not grant any access.

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

## Level 7 → 8
**Goal:** the password is next to the word `millionth` in `data.txt`.

`grep` shows lines that contain a word or pattern.

```bash
grep millionth data.txt
```

## Level 8 → 9
**Goal:** the password is the only line in `data.txt` that appears once.

- `sort` orders lines alphabetically.
- `uniq` collapses repeated lines, but only neighbouring ones, so always sort first.
- `uniq -u` shows only lines that appear once. `uniq -c` shows counts.
- `|` (pipe) sends one command's output into the next.

```bash
sort data.txt | uniq -u
```

## Level 9 → 10
**Goal:** the password is in one of the few human-readable strings in `data.txt`, preceded by several `=` characters.

`strings` prints only the readable text inside a file. Pipe it into `grep` to filter.

```bash
strings data.txt | grep "=="
```

## Level 10 → 11
**Goal:** `data.txt` contains base64-encoded data.

`base64 -d` decodes it. Base64 is an encoding, not encryption.

```bash
base64 -d data.txt
```

## Level 11 → 12 (in progress)
**Goal:** `data.txt` has all letters rotated by 13 positions (ROT13).
