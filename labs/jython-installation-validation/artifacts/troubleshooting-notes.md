# Jython Installation & Validation — Troubleshooting Notes

**Author:** Ivan Rozenblad
**Type:** Tooling lab — troubleshooting log
**Environment:** macOS; Java 8+ JDK/JRE on `PATH`
**Parent lab:** [`../README.md`](../README.md)

These are the install/launch failure modes I accounted for while installing and validating
**Jython 2.7.4**, with the symptom, root cause, and the resolution for each. Jython 2.7.4
requires **Java 8 as the minimum** and is tested against Java 8 and Java 11; several issues
below trace back to the Java runtime on `PATH`.

---

## Issue Log

| # | Symptom | Cause | Resolution |
|---|---|---|---|
| 1 | `jython: command not found` | The installer places the `jython` launcher in the install's `bin` directory; it is **not** added to `PATH` automatically. | Invoke the launcher by full path, or add the install `bin` dir to `PATH`, e.g. `export PATH=/opt/jython/bin:$PATH`. On Windows the launcher is `jython.exe` (plus `jython.bat`) in the install directory. |
| 2 | `Error: Unable to access jarfile <name>.jar` | `java -jar` was pointed at a wrong path/filename, or the JAR is in a different directory, or the name/version doesn't match what was typed. | `cd` to the download directory and pass the exact filename (e.g. `jython-installer-2.7.4.jar`); verify with a directory listing first. |
| 3 | `java.lang.UnsupportedClassVersionError` ("Unsupported major.minor version") | The JRE running the code is **older** than required — the class file's bytecode major version exceeds what the running JVM supports. For Jython this appears when `java` on `PATH` is older than the Java 8 minimum. | Point `JAVA_HOME`/`PATH` at a new-enough JDK/JRE (Java 8+), or run the installer with `-j`/`--jre` set to a compatible runtime. Major-version map: `52` = Java 8, `55` = Java 11. |
| 4 | `NoClassDefFoundError` when launching the installer JAR (e.g. `Unable to initialize main class org.python.util.install.Installation … InstallationCancelledException`) | Typically a corrupt or incompletely downloaded installer JAR, or a mismatched/broken `java` on `PATH`. | Re-download the installer JAR and re-verify, and confirm which `java` is actually being invoked. (Tracked as an open Jython GitHub issue.) |
| 5 | Launcher can't find a JVM / Java not resolved | `JAVA_HOME` / `PATH` not set correctly — Jython's launcher relies on a Java runtime being resolvable. | Linux/macOS: `export JAVA_HOME=/path/to/jdk` and `export PATH=$JAVA_HOME/bin:$PATH`. Windows: `set JAVA_HOME=…` and update `PATH`. Alternatively bake the runtime into the generated launcher with the installer's `-j`/`--jre <dir>` (executables assumed under `/bin`). |
| 6 | GUI installer fails on a headless box / over SSH (no display) | The default `java -jar jython-installer-2.7.4.jar` opens the GUI installer, which has no display to attach to. | Force the console installer with `--console` (`-c`), or run an unattended silent install: `java -jar jython-installer-2.7.4.jar -s -d /path/to/dir -t standard` — silent mode **requires** `-d`. |
| 7 | Non-ASCII output garbled / `UnicodeEncodeError` on the Windows console | The Windows console's default OEM/ANSI code page mangles non-ASCII output. | `chcp 65001` switches the console to UTF-8 and helps **stdout**, but it does not fix `argv` or file-open, which still use the ANSI code page; expect argv/filename edge cases to persist. |

---

## Environment

Record the actual values from the host used, so the run is reproducible:

- **OS:** _____________________ (this lab: macOS)
- **JDK/JRE version** — capture from:

  ```bash
  java -version
  ```

  ```
  # paste actual output here
  ```

- **Jython version** — capture from (string is printed to stderr):

  ```bash
  jython --version
  ```

  ```
  Jython 2.7.4
  ```

---

## Validation Checklist

- [ ] `java -version` reports a Java 8+ runtime resolvable on `PATH`.
- [ ] Jython installed from an official Maven Central artifact (installer or standalone JAR) — not via `pip`/OS package manager.
- [ ] `jython --version` prints `Jython 2.7.4`.
- [ ] REPL startup banner names both the Jython version and the underlying JVM (`… on java…`).
- [ ] `import sys; print(sys.version)` returns the version, and `sys.platform` is a `java…` value.
- [ ] Java interop smoke test (`from java.lang import System; System.out.println("Hola")`) prints without a traceback.
- [ ] A trivial `.py` script runs end-to-end via `jython script.py` (or the standalone JAR).

---

*Lab performed in a controlled environment for educational and portfolio purposes.*
