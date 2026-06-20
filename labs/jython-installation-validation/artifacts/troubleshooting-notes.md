# Troubleshooting Notes — Jython Installation & Validation

**Status:** 🚧 Placeholder — to be filled in with notes from the lab session.

Record issues encountered and their resolutions here. Suggested structure:

## Issue Log

| # | Symptom | Cause | Resolution |
|---|---------|-------|------------|
| 1 | _e.g. `java: command not found`_ | _JDK not on PATH_ | _Set `JAVA_HOME` and add `$JAVA_HOME/bin` to PATH_ |

## Environment

- OS:
- JDK version (`java -version`):
- Jython version (`jython --version`):

## Validation Checklist

- [ ] `java -version` returns a supported JDK
- [ ] Jython interactive shell launches
- [ ] `import sys; print(sys.version)` runs without error
- [ ] Sample script executes successfully
