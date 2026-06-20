# Linux Permissions Lab — Applying Least Privilege with `chmod`

**Author:** Ivan Rozenblad
**Type:** Linux file-permissions lab
**Environment:** Bash shell, Linux
**Working directory:** `/home/researcher2/projects`

---

## Executive Summary

As a security professional supporting a research team, I audited and corrected file and
directory permissions in a shared `projects` directory. Several files granted more access
than the team's policy allowed — including write access to "group" and "other," and an
archive directory that others could enter. I used `ls -la` to inspect the current
permission strings and `chmod` to bring each file in line with the principle of **least
privilege**, ensuring users have only the access their role requires.

---

## Objectives

- Read and interpret Linux permission strings.
- Identify files whose permissions exceed the authorized level.
- Remove unauthorized read, write, and execute access using `chmod`.
- Verify each change.

---

## Background: Reading a Permission String

`ls -la` shows a 10-character mode string, e.g. `-rw-rw-r--`:

| Position | Meaning |
|---|---|
| 1 | File type — `-` file, `d` directory |
| 2–4 | **User (owner)** permissions: read `r`, write `w`, execute `x` |
| 5–7 | **Group** permissions |
| 8–10 | **Other** (everyone else) permissions |

A dash (`-`) in any slot means that permission is not granted.

---

## Procedure

### 1. Check the current permissions

```bash
ls -la
```

Example output for the project directory:

```
drwxr-xr-x  2 researcher2 research_team  4096 ...  .
drwxr-xr-x  3 researcher2 research_team  4096 ...  ..
-rw-rw-rw-  1 researcher2 research_team   ...  project_k.txt
-rw-r-----  1 researcher2 research_team   ...  project_m.txt
-rw-rw-r--  1 researcher2 research_team   ...  project_r.txt
-rw-rw-r--  1 researcher2 research_team   ...  project_t.txt
drwxr-xr-x  2 researcher2 research_team   ...  drafts
```

Note that hidden files (such as `.project_x.txt`) require the `-a` flag to appear, which
is why `ls -la` is used instead of `ls -l`.

### 2. Remove unauthorized write access from "other"

`project_k.txt` showed `-rw-rw-rw-`, granting **write** access to everyone. Policy allows
write only for the owner and group, so I removed write from "other":

```bash
chmod o-w project_k.txt
```

Result: `-rw-rw-r--`.

### 3. Remove unauthorized read access from "group"

`project_m.txt` was intended to be readable only by the owner, but the group could read it.
I removed read and write from group (and ensured "other" has none):

```bash
chmod g-r project_m.txt
```

Result: `-rw-------` (owner read/write only), matching the access policy for that file.

### 4. Modify directory permissions

The hidden `drafts` directory should be accessible only to the owner (`researcher2`).
The `x` (execute) bit on a directory controls whether a user can **enter** it, so I
removed group execute:

```bash
chmod g-x drafts
```

Result: `drwxr-x---` → after change `drwxr-----`, so only the owner can `cd` into and
traverse `drafts`.

### 5. Verify

```bash
ls -la
```

I re-ran `ls -la` after each change and confirmed every mode string matched the intended
access level.

---

## `chmod` Quick Reference (symbolic mode)

| Target | Meaning |
|---|---|
| `u` | user / owner |
| `g` | group |
| `o` | other |
| `a` | all |

| Operator | Effect |
|---|---|
| `+` | add permission |
| `-` | remove permission |
| `=` | set exactly |

Example: `chmod u+rwx,g-w,o-rwx file` sets full owner access, removes group write, and
removes all access for others.

---

## Security Considerations

- **Least privilege:** each file should grant the minimum access required. World-writable
  files (`-rw-rw-rw-`) are a common misconfiguration that lets any local user tamper with
  data.
- **Directory `x` ≠ file `x`:** on a directory, the execute bit governs traversal, not code
  execution — removing it from group/other is how you stop unauthorized users from entering
  a folder.
- **Verify, don't assume:** always confirm with `ls -la` after a change; a wrong `chmod`
  can silently over- or under-grant access.

---

## Results

| File / dir | Before | Action | After |
|---|---|---|---|
| `project_k.txt` | `-rw-rw-rw-` | `chmod o-w` | `-rw-rw-r--` |
| `project_m.txt` | `-rw-r-----` | `chmod g-r` | `-rw-------` |
| `drafts/` | `drwxr-x---` | `chmod g-x` | `drwxr-----` |

All files in `/home/researcher2/projects` now conform to the team's authorized access
levels.

---

*Performed in a controlled lab environment. Paths and filenames are from a training
scenario; no production systems were modified.*
