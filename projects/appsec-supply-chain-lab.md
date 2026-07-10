# AppSec Supply Chain Lab

**Repo:** [IRsoctierDT/portfolio-appsec-lab](https://github.com/IRsoctierDT/portfolio-appsec-lab)
**Status:** 🚧 In progress — environment design phase

---

## What it is

A localized Application Security (AppSec) lab environment designed to **detect and
remediate software supply chain vulnerabilities across multiple package ecosystems**
(npm, PyPI, and friends).

## Planned artifact set

- Dependency-confusion and typosquatting detection exercises
- SBOM-driven vulnerability management workflow (generate → diff → prioritize)
- Vulnerable-dependency remediation playbooks with before/after evidence
- CI security gate configurations (secret scanning, dependency audit, SAST) that mirror
  the pipelines already running in my active projects

## Why it matters

Supply chain compromise is one of the highest-leverage attack classes today, and the
skills transfer directly from the release-engineering work in
[MCPscan](./ai-agentic-mcpscan.md) (SBOM + checksums on every release, pip-audit in CI)
and the governance pipeline in the
[Cyber Command Center](./ai-operator-cyber-command-center.md). This lab turns those
practices into standalone, reproducible artifacts.
