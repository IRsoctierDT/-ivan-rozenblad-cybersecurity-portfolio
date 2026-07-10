# AI Agentic MCPscan

**Repo:** [IRsoctierDT/ai-agentic-mcpscan](https://github.com/IRsoctierDT/ai-agentic-mcpscan)
**Released:** [PyPI — `ai-agentic-mcpscan`](https://pypi.org/project/ai-agentic-mcpscan/) (v0.10.0, declared stable for 1.0 — stable CLI surface, JSON schema, and check ids under semver) · Apache-2.0
**Stack:** Python 3.11+ · CLI (`mcpscan`) · CI on macOS/Linux/Windows × Python 3.11–3.13

---

## What it is

A **local-first, offline-by-default security posture scanner** for MCP servers and local
AI-agent setups. As organizations wire AI agents into their machines through the Model
Context Protocol, they inherit a new attack surface — exposed local servers, plaintext
API keys in agent configs, over-broad tool scopes, unpinned `npx`/`uvx` packages.
MCPscan finds those issues and tells you which to fix first.

## What it does

- **Discovers** MCP servers via socket/process enumeration (catching `0.0.0.0` /
  non-loopback exposure) plus a loopback probe of `/mcp` and `/sse`.
- **Statically audits** agent configs across **seven host ecosystems** — Claude
  (`.claude/settings.json`, `.mcp.json`, `claude_desktop_config.json`), **Cursor**,
  **Windsurf**, **Cline**, **VS Code** (native MCP), **Zed** (JSONC), and **Continue**
  (YAML) — plus `.env` files, for plaintext secrets, auto-approval flags, over-broad
  tool scopes, and unpinned versions.
- **Scores** each server **A–F** across four dimensions: exposure, credential hygiene,
  tool-scope breadth, and version pinning.
- **Reports** prioritized, redacted remediation in four forms — terminal, self-contained
  HTML, stable JSON, and **SARIF 2.1.0 for GitHub code scanning** — with a `--fail-on`
  severity gate that drops straight into CI.
- **Fixes** over-broad tool-scope grants with an opt-in `--fix` that applies only safe,
  reversible edits and backs up every file it touches first.
- **Scans authorized LANs** via a separate `mcpscan lan` command built on an
  authorization-first safety core, with an enterprise-policy gate for public targets and
  optional Ed25519 manifest verification (`[crypto]` extra).

## Security engineering demonstrated

- **Threat-model-driven build** — full product spec with testable requirements and
  scoring rubric ([SPEC.md](https://github.com/IRsoctierDT/ai-agentic-mcpscan/blob/main/docs/SPEC.md)),
  15 architecture decision records, and a threat-model verification matrix signed off in
  [SECURITY_SIGNOFF.md](https://github.com/IRsoctierDT/ai-agentic-mcpscan/blob/main/docs/SECURITY_SIGNOFF.md).
- **Trust properties by design** — localhost only by default; offline + zero telemetry
  by default (`--online` is opt-in and discloses egress); secrets redacted everywhere;
  advise-only unless `--fix` is explicitly passed (safe, reversible, backed-up edits
  only); stateless; **passes its own scan**.
- **Authorization-first LAN scanning** — network scanning is a separate command gated on
  explicit authorization, with an enterprise-policy gate before any public target is
  touched and an operator guide documenting lawful use.
- **Release engineering** — semantic-versioned releases via release-please, SBOM +
  checksums on every release, green CI gate (ruff, mypy --strict, bandit, pytest) across
  three OSes and three Python versions, and a measurable dogfood corpus harness as a
  pre-1.0 quality gate.

## Road to 1.0 — shipped

The entire 1.0 feature set is built and declared stable: SARIF output + GitHub
code-scanning workflow, seven host adapters, opt-in `--fix`, and authorized-LAN scanning
behind an explicit policy gate. Ten minor releases (v0.1.0 → v0.10.0), each shipped
behind the full CI gate. Next: real-world dogfooding and keeping pace with the
fast-moving MCP ecosystem.
