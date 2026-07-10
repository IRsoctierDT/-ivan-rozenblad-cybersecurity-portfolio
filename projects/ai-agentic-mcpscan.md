# AI Agentic MCPscan

**Repo:** [IRsoctierDT/ai-agentic-mcpscan](https://github.com/IRsoctierDT/ai-agentic-mcpscan)
**Released:** [PyPI — `ai-agentic-mcpscan`](https://pypi.org/project/ai-agentic-mcpscan/) (Beta, v0.3.0) · Apache-2.0
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
- **Statically audits** agent configs across the ecosystem — Claude
  (`.claude/settings.json`, `.mcp.json`, `claude_desktop_config.json`), **Cursor**,
  **Windsurf**, and **Cline** — plus `.env` files, for plaintext secrets, auto-approval
  flags, over-broad tool scopes, and unpinned versions.
- **Scores** each server **A–F** across four dimensions: exposure, credential hygiene,
  tool-scope breadth, and version pinning.
- **Reports** prioritized, redacted, advise-only remediation in three forms — terminal,
  self-contained HTML, and stable JSON — with a `--fail-on` severity gate that drops
  straight into CI.

## Security engineering demonstrated

- **Threat-model-driven build** — full product spec with testable requirements and
  scoring rubric ([SPEC.md](https://github.com/IRsoctierDT/ai-agentic-mcpscan/blob/main/docs/SPEC.md)),
  15 architecture decision records, and a threat-model verification matrix signed off in
  [SECURITY_SIGNOFF.md](https://github.com/IRsoctierDT/ai-agentic-mcpscan/blob/main/docs/SECURITY_SIGNOFF.md).
- **Trust properties by design** — localhost only; offline + zero telemetry by default
  (`--online` is opt-in and discloses egress); secrets redacted everywhere; advise-only
  (never writes to configs); stateless; **passes its own scan**.
- **Release engineering** — semantic-versioned releases via release-please, SBOM +
  checksums on every release, green CI gate (ruff, mypy --strict, bandit, pytest) across
  three OSes and three Python versions.

## Roadmap to 1.0

Real-world dogfooding, SARIF output + a GitHub code-scanning action, more host adapters,
opt-in `--fix`, and authorized-LAN scanning behind an explicit gate.
