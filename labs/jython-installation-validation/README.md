# Jython Installation & Validation

**Author:** Ivan Rozenblad
**Type:** Tooling lab — installation & environment validation
**Environment:** macOS; Java 8+ JDK/JRE on `PATH`
**Status:** ✅ Writeup complete — screenshots pending

---

## Executive Summary

As part of building out a tooling lab, I installed and validated **Jython** — an
implementation of the Python language that runs on the Java Virtual Machine (JVM). Unlike
CPython, Jython is not fetched from PyPI or an OS package manager: it ships as JAR
artifacts from Maven Central and runs on top of a Java runtime, which makes it useful for
scripting against Java libraries and embedding a Python interpreter inside JVM
applications.

This lab documents a clean, repeatable install of the current stable release
(**Jython 2.7.4**, tagged final on 18 August 2024), followed by a layered validation pass:
confirming the interpreter version, reading the startup banner to verify which JVM it bound
to, checking the version programmatically through the `sys` module, and running a
Python-to-Java interop smoke test to prove the language bridge is live. A short
troubleshooting section captures the failure modes I accounted for; the full issue log
lives in [`./artifacts/troubleshooting-notes.md`](./artifacts/troubleshooting-notes.md).

> **Note on the language version:** Jython 2.7.x implements **Python 2.7 only** — there is
> no released Python 3 (Jython 3.x) line as of 2.7.4. Python 2.7 (the language) is no longer
> supported by the Python Software Foundation, so I treat Jython here as a JVM-scripting and
> interop tool for a lab context, not as a general-purpose modern Python runtime.

---

## Objectives

- Confirm the prerequisites (a Java 8+ runtime resolvable on `PATH`) before installing.
- Install Jython 2.7.4 from an official Maven Central artifact, using a repeatable,
  non-interactive method where possible.
- Verify the installed interpreter version (`jython --version`).
- Read the REPL startup banner to confirm both the Jython version and the underlying JVM.
- Confirm the version programmatically via the `sys` module.
- Prove the Python-to-Java bridge works with a `java.lang` interop smoke test.
- Run a trivial `.py` script end-to-end as functional validation.

---

## Prerequisites

| Requirement | Detail |
|---|---|
| **Java runtime** | Jython 2.7.4 requires **Java 8 as the minimum** and is tested against Java 8 and Java 11. A JRE is sufficient to *run* Jython; a JDK is only needed to compile/build. |
| **`java` on `PATH`** | The launcher relies on a Java runtime being resolvable. Confirm with `java -version` before starting. |
| **Distribution artifact** | Jython is delivered as JARs from **Maven Central** (group `org.python`) — the **installer JAR** (`jython-installer-2.7.4.jar`) or the **standalone JAR** (`jython-standalone-2.7.4.jar`). It is **not** installed via `pip` or an OS package manager. |

Verify the Java runtime first:

```bash
java -version
```

If `java` is not found, or reports a version older than 8, resolve that before continuing
(see [Troubleshooting](#troubleshooting)). Jython 2.7.4 also includes Java 21 compatibility
fixes and ships its JARs as automatic modules for use in modular (JPMS) builds.

---

## Installation

Jython offers two delivery models. I document both; either produces a working interpreter.

### Option A — Installer JAR (installs Jython as a local application)

The installer is launched with `java -jar`. With no flags it opens a **GUI installer** on
desktop systems (or a console installer on headless systems):

```bash
java -jar jython-installer-2.7.4.jar
```

For a headless box or an SSH session, force the text-based **console** installer:

```bash
java -jar jython-installer-2.7.4.jar --console      # short form: -c
```

For a fully unattended install, use **silent** mode. Silent mode **requires** a target
directory (`-d`); `-t` selects the install type:

```bash
java -jar jython-installer-2.7.4.jar -s -d /opt/jython -t standard
```

Installer flags:

| Flag | Meaning |
|---|---|
| `-c`, `--console` | Text-based interactive install (headless-friendly) |
| `-s`, `--silent` | Non-interactive install (**requires** `-d`) |
| `-d`, `--directory <dir>` | Target install directory |
| `-t`, `--type <type>` | `standard` (core+mod+demo+doc), `minimum` (core only), `all` (everything incl. src), or `standalone` (single executable `jython.jar`) |
| `--help` | List all options |

As its final step, the installer runs `jython -m ensurepip` to provision **pip** and
**setuptools** by default — this is for installing Python packages *into* Jython, not for
installing Jython itself. After install, the interpreter is launched via the generated
launcher in the install's `bin` directory: `bin/jython` on Unix-like systems, and
`jython.bat` plus a native `bin/jython.exe` on Windows.

### Option B — Standalone JAR (no install step)

The standalone JAR runs Jython directly, with no install. It embeds the Python standard
library and can also sit on a Java application's classpath to embed Jython:

```bash
# Interactive interpreter
java -jar jython-standalone-2.7.4.jar

# Run a script
java -jar jython-standalone-2.7.4.jar script.py
```

> **Which to choose:** I used the installer JAR when I wanted a persistent install with a
> `bin/jython` launcher and bundled pip; I used the standalone JAR for quick, disposable
> runs and for classpath embedding. The standalone JAR avoids cache setup, so it starts
> faster at some cost to Java class-call performance.

### A note on the runtime "registry"

At startup Jython locates its root directory from the Java system property `python.home`,
falling back to `install.root`, and finally to locating `jython.jar` on the classpath. It
then reads `rootdir/registry` (a file of `prop=value` pairs), sets `sys.prefix` /
`sys.exec_prefix` to that root, and appends `rootdir/Lib` to `sys.path`. A per-user
overrides file of the same form is read from `user.home/.jython`. Properties are commonly
set on the Java command line with `-D`, e.g. `-Dpython.home=...` or `-Dpython.path=...`.

---

## Validation

I validated the install in layers, from a simple version check up to a live Python-to-Java
call. If the standalone JAR was used instead of the installer, substitute
`java -jar jython-standalone-2.7.4.jar` for the `jython` launcher in each step.

### 1. Interpreter version

```bash
jython --version
```

Expected output (note: like CPython 2.7's launcher, the version string is written to
**stderr**, and the exact string reflects the installed release):

```
Jython 2.7.4
```

### 2. REPL startup banner

Launching the interpreter with no arguments starts the console. The banner names both the
Jython version and the JVM actually running it — a fast confirmation the Java bridge
initialized:

```bash
jython
```

Expected banner (representative — the bracketed VM name and trailing `on java…` reflect the
JRE actually in use on the host):

```pycon
Jython 2.7.4 (tags/v2.7.4:3f256f4a7, Aug 18 2024, 10:30:53)
[Java HotSpot(TM) 64-Bit Server VM (Oracle Corporation)] on java...
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

### 3. Version via the `sys` module (scriptable equivalent)

The same version string is available programmatically, and `sys.platform` returns a
`java`-prefixed value:

```pycon
>>> import sys
>>> print(sys.version)
2.7.4 ...
>>> sys.platform
'java...'
```

The standard-library `platform` module is also present in Jython's `Lib`;
`platform.java_ver()` reports the JVM version, vendor, and OS.

### 4. Python-to-Java interop smoke test

Importing a `java.lang` class and calling a Java method proves the Python-to-Java bridge is
live. If this runs without a traceback and prints the string, the classpath and interop
layer are healthy:

```pycon
>>> from java.lang import System
>>> System.out.println("Hola")
Hola
```

To inspect the live JVM configuration, read Java system properties directly:

```pycon
>>> from java.lang import System
>>> props = System.getProperties()   # e.g. java.version, java.home, os.name
```

### 5. Run a script end-to-end

Finally, functional validation with a trivial script (`test.py`):

```python
from java.lang import System

System.out.println("Hello from Jython")
print("ok")
```

```bash
jython test.py
# or, with the standalone JAR:
java -jar jython-standalone-2.7.4.jar test.py
```

Expected output:

```
Hello from Jython
ok
```

### Validation results

| # | Check | Command | Expected result |
|---|---|---|---|
| 1 | Interpreter version | `jython --version` | `Jython 2.7.4` (printed to stderr) |
| 2 | Startup banner | `jython` | Banner naming Jython 2.7.4 **and** the running JVM (`… on java…`) |
| 3 | Version via `sys` | `import sys; print(sys.version)` | Same version info; `sys.platform` is `java…` |
| 4 | Java interop | `from java.lang import System; System.out.println("Hola")` | Prints `Hola`, no traceback |
| 5 | Script execution | `jython test.py` | Prints the script's output (`Hello from Jython` / `ok`) |

---

## Troubleshooting

Common install/launch failures and their fixes are documented separately in
[`./artifacts/troubleshooting-notes.md`](./artifacts/troubleshooting-notes.md). In brief:

- **`jython: command not found`** — the install `bin` directory is not on `PATH`; invoke by
  full path or add it (`export PATH=/opt/jython/bin:$PATH`).
- **`Error: Unable to access jarfile …`** — wrong path or filename; `cd` to the download
  directory and pass the exact filename.
- **`java.lang.UnsupportedClassVersionError`** — the `java` on `PATH` is older than the
  Java 8 minimum; point `JAVA_HOME`/`PATH` at a new-enough runtime.
- **`NoClassDefFoundError` launching the installer** — typically a corrupt/incomplete
  installer download or a broken `java`; re-download and verify the `java` being invoked.
- **GUI installer fails over SSH / headless** — use `--console` (`-c`) or silent mode.
- **Windows console encoding** — `chcp 65001` helps stdout but not argv/filenames.

---

## Screenshots

Screenshots for this lab are pending. The three planned captures:

| File | Shows |
|---|---|
| `java-version.png` | Output of `java -version`, confirming a Java 8+ runtime on `PATH` |
| `jython-startup.png` | The Jython REPL startup banner naming both the Jython and JVM versions |
| `validation-tests.png` | The `sys.version` check and the `java.lang.System` interop smoke test |

> The PNGs are to be dropped into `./screenshots/`, and this placeholder note replaced with
> the embedded images once captured.

---

*Lab performed in a controlled environment for educational and portfolio purposes.*
