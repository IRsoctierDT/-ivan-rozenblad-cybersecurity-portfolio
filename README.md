# Ivan Rozenblad — Cybersecurity Portfolio

> **Security engineering at the intersection of AI and defense — built, shipped, and proven.**

A working portfolio of hands-on cybersecurity engineering: AI-driven SOC automation,
published open-source security tooling, NIST CSF-aligned risk assessment and auditing,
network traffic analysis, incident response, and system hardening. Every artifact here
is built the way production security work should be — **threat-modeled, documented,
tested behind CI security gates, and reproducible** — because a control that isn't
documented and testable isn't a control.

> **Focus areas:** AI × defensive security · Security automation & detection engineering · Risk & audit · Network defense · Incident response

---

## About Me

I'm Ivan Rozenblad, a cybersecurity practitioner and technology consultant based in the
San Francisco Bay Area. I came to security the operator's way — through years of
hands-on network engineering, systems work, and consulting — and that path left me with
the conviction that runs through everything in this portfolio: **security only works
when it's engineered in, not bolted on.** Controls have to be designed, documented,
tested, and auditable, or they don't survive contact with a real environment.

What distinguishes my work:

- **I ship, not just study.** My security tooling is published and installable today:
  [MCPscan](./projects/ianua-broker-mcpscan.md) is **stable v1.x** on
  [PyPI](https://pypi.org/project/ai-agentic-mcpscan/) with SBOM'd, checksummed releases
  behind a cross-platform CI gate, and [IANUA](./projects/ianua.md) is a fully built SOC
  automation platform documented in eleven reproducible case studies.
- **I work both sides of the AI/security boundary.** Using AI to scale defense —
  agentic log triage, MITRE ATT&CK mapping, RAG-grounded incident reporting — and
  securing the AI-agent ecosystem itself: MCP posture scanning, zero-trust agent
  identity ([Agent Trust Broker](./projects/agent-trust-broker.md)), policy-gated tool
  surfaces, and tamper-evident (hash-chained, Ed25519-signed) audit logging.
- **I write the standard, then implement it.** [EAODS](./projects/eaods.md) is my
  enterprise governance framework for AI-assisted organizations; its zero-trust identity
  pattern is reference-implemented by the Agent Trust Broker and enforced on every tool
  dispatch inside IANUA — a full standard → control → implementation → conformance-test
  chain.
- **I run what I recommend.** My home security lab — pfSense (Netgate 4200), UniFi
  infrastructure, VLAN segmentation, Suricata IDS/IPS, pfBlockerNG, and Unbound DNS —
  is where every detection rule, hardening change, and network policy gets tested
  before I write about it.
- **Governance-first engineering.** Written threat models, architecture decision
  records, default-deny policy-as-code, human-in-the-loop gates for anything
  irreversible, and CI pipelines that treat security as a quality gate: bandit,
  gitleaks, pip-audit, ruff, mypy --strict, and enforced coverage thresholds.
- **I document like an auditor is reading.** Executive summaries, structured incident
  reports, audit-scoped risk assessments, and case studies with worked examples — every
  deliverable in this portfolio is written to be handed to a client, a reviewer, or a
  hiring manager as-is.

**Career direction:** Security Engineer · SOC / Detection Engineer · AI Security Engineer — open to consulting engagements.

See my full [Professional Statement](./professional-statement.md) for my security
philosophy, what I'm building right now, and where I'm headed.

---

## 🚀 Active Projects

Flagship work lives in dedicated repositories, summarized as artifacts in [`projects/`](./projects/):

Most of this work ships under the **IANUA** umbrella — a platform, a scanner, a
zero-trust identity layer, and the governance framework that binds them.

| Project | Status | What it demonstrates |
|---|---|---|
| [IANUA — AI Operations & Cyber Command Center](./projects/ianua.md) | Active — all agents built; zero-trust + compliance layers landing | Local-first SOC automation: agentic triage (0–100 severity), MITRE ATT&CK mapping, threat-intel enrichment, RAG pipeline, policy-gated MCP tools with a trust-broker identity gate, Ed25519-signed tamper-evident audit log, Sigma correlation rules, compliance layer (controls, evidence, trust page), pending-approvals queue. Eleven reproducible case studies. |
| [IANUA-Broker — AI Agentic MCPscan](./projects/ianua-broker-mcpscan.md) | **Stable v1.x** (v1.4.0) [on PyPI](https://pypi.org/project/ai-agentic-mcpscan/) | Offline-by-default posture scanner + AI-asset inventory for MCP/AI-agent setups: 7 host adapters (Claude, Cursor, Windsurf, Cline, VS Code, Zed, Continue), A–F grading, SARIF 2.1.0 + GitHub code scanning, opt-in `--fix`, authorization-gated LAN scanning; threat-model-driven spec, SBOM'd releases, cross-platform CI + CodeQL. |
| [Agent Trust Broker](./projects/agent-trust-broker.md) | Active — v0.1 reference implementation, wired into IANUA | Zero-trust identity for AI-agent fleets: short-lived scoped identities, attenuating delegation, allow/deny/escalate policy, hash-chained audit with human escalation queue, T1–T12 conformance test matrix. Fail-closed, stdlib-only. |
| [EAODS — Enterprise AI Operator Documentation Suite](./projects/eaods.md) | Active — release line v17.0–v17.3 | Enterprise architecture, governance & cyber-defense framework for AI-assisted organizations, with schema-validated docs, traceability, and CI quality gates; patterns trace into running code (ATB → IANUA). |
| [AppSec Supply Chain Lab](./projects/appsec-supply-chain-lab.md) | 🚧 In progress | Detecting & remediating software supply chain vulnerabilities across package ecosystems. |

---

## Repository Structure

```
cybersecurity-portfolio/
├── README.md
├── professional-statement.md
├── projects/                   # Artifacts for flagship external repos
│   ├── ianua.md                      # IANUA — AI ops & cyber command center
│   ├── ianua-broker-mcpscan.md       # IANUA-Broker — MCPscan (stable v1.x, PyPI)
│   ├── agent-trust-broker.md         # Zero-trust identity for agent fleets
│   ├── eaods.md                      # Enterprise AI governance framework
│   └── appsec-supply-chain-lab.md
├── labs/                       # Hands-on technical labs (one folder per lab)
│   ├── secure-query-lab/             # SQL filtering for log investigation
│   ├── linux-permissions-lab/        # Linux file permissions & least privilege
│   └── jython-installation-validation/  # Jython (Python on the JVM) — in progress
├── incident-response/          # Incident analysis & response deliverables
├── network-security/           # Traffic analysis, packet capture, hardening
├── risk-assessment/            # Security risk assessments & NIST CSF audits
├── threat-intelligence/        # IOC triage & ATT&CK mapping (via command center)
├── malware-analysis/           # Static/dynamic analysis in isolated lab (planned)
└── security-automation/        # SOC automation & security tooling (active)
```

---

## Domains

| Domain | Contents |
|---|---|
| [projects](./projects/) | IANUA, IANUA-Broker (MCPscan), Agent Trust Broker, EAODS, AppSec supply chain lab |
| [security-automation](./security-automation/) | Agentic SOC triage, Sigma correlation loop, zero-trust tool gating, MCP posture scanning in CI |
| [threat-intelligence](./threat-intelligence/) | IOC triage agent, MITRE ATT&CK mapper, Sigma correlation rules (case studies) |
| [labs](./labs/) | SQL filtering, Linux permissions, Jython install & validation |
| [incident-response](./incident-response/) | DNS/ICMP outage and network-traffic incident reports |
| [network-security](./network-security/) | Packet-capture analysis writeup, `.pcapng` capture, hardening catalog |
| [risk-assessment](./risk-assessment/) | Botium Toys audit, audit scope & goals, risk assessment reports (NIST CSF) |
| [malware-analysis](./malware-analysis/) | 🚧 Planned |

---

## Build & Release Status

Live build, release, and license status for my flagship public repositories — the "what it
does" details and case studies are in [🚀 Active Projects](#-active-projects) above. Every
badge reads live from GitHub, so this table stays current on its own.

| Repository | Version / Release | CI & Security | License |
|---|---|---|---|
| **[IANUA](https://github.com/IRsoctierDT/IANUA)** | [![release](https://img.shields.io/github/v/release/IRsoctierDT/IANUA?sort=semver&label=)](https://github.com/IRsoctierDT/IANUA/releases) | [![CI](https://github.com/IRsoctierDT/IANUA/actions/workflows/ci.yml/badge.svg)](https://github.com/IRsoctierDT/IANUA/actions/workflows/ci.yml) [![Security](https://github.com/IRsoctierDT/IANUA/actions/workflows/security-scan.yml/badge.svg)](https://github.com/IRsoctierDT/IANUA/actions/workflows/security-scan.yml) | ![last commit](https://img.shields.io/github/last-commit/IRsoctierDT/IANUA?label=updated) |
| **[IANUA-Broker](https://github.com/IRsoctierDT/IANUA-Broker)** | [![release](https://img.shields.io/github/v/release/IRsoctierDT/IANUA-Broker?label=)](https://github.com/IRsoctierDT/IANUA-Broker/releases) [![PyPI](https://img.shields.io/pypi/v/ai-agentic-mcpscan?label=PyPI)](https://pypi.org/project/ai-agentic-mcpscan/) | [![CI](https://github.com/IRsoctierDT/IANUA-Broker/actions/workflows/ci.yml/badge.svg)](https://github.com/IRsoctierDT/IANUA-Broker/actions/workflows/ci.yml) [![CodeQL](https://github.com/IRsoctierDT/IANUA-Broker/actions/workflows/codeql.yml/badge.svg)](https://github.com/IRsoctierDT/IANUA-Broker/actions/workflows/codeql.yml) | [![license](https://img.shields.io/github/license/IRsoctierDT/IANUA-Broker?label=)](https://github.com/IRsoctierDT/IANUA-Broker/blob/main/LICENSE) |
| **[agent-trust-broker](https://github.com/IRsoctierDT/agent-trust-broker)** | ![status](https://img.shields.io/badge/release-v0.1%20(unreleased)-lightgrey) | [![Quality](https://github.com/IRsoctierDT/agent-trust-broker/actions/workflows/quality.yml/badge.svg)](https://github.com/IRsoctierDT/agent-trust-broker/actions/workflows/quality.yml) [![CodeQL](https://github.com/IRsoctierDT/agent-trust-broker/actions/workflows/codeql.yml/badge.svg)](https://github.com/IRsoctierDT/agent-trust-broker/actions/workflows/codeql.yml) | [![license](https://img.shields.io/github/license/IRsoctierDT/agent-trust-broker?label=)](https://github.com/IRsoctierDT/agent-trust-broker/blob/main/LICENSE) |
| **[EAODS-v3-Enterprise-Edition](https://github.com/IRsoctierDT/EAODS-v3-Enterprise-Edition)** | ![status](https://img.shields.io/badge/status-active-brightgreen) | [![Docs quality](https://github.com/IRsoctierDT/EAODS-v3-Enterprise-Edition/actions/workflows/docs-quality.yml/badge.svg)](https://github.com/IRsoctierDT/EAODS-v3-Enterprise-Edition/actions/workflows/docs-quality.yml) [![Pages](https://github.com/IRsoctierDT/EAODS-v3-Enterprise-Edition/actions/workflows/pages.yml/badge.svg)](https://github.com/IRsoctierDT/EAODS-v3-Enterprise-Edition/actions/workflows/pages.yml) | ![last commit](https://img.shields.io/github/last-commit/IRsoctierDT/EAODS-v3-Enterprise-Edition?label=updated) |

- **IANUA** ships signed, reproducible builds — latest release **v1.9.0** carries CycloneDX SBOM + SLSA build-provenance attestations, 390 tests green behind an ≥85% coverage gate.
- **IANUA-Broker / MCPscan** cuts releases automatically via release-please, published to [PyPI](https://pypi.org/project/ai-agentic-mcpscan/) with CodeQL scanning and an SBOM on every build.

> _Note:_ the public repos `EAODS` and `portfolio-appsec-lab` are currently empty
> scaffolding (no released content yet), so they're omitted from this table.

---

## Skills Demonstrated

| Domain | Highlights |
|---|---|
| AI Security & Automation | Agentic SOC pipelines, RAG knowledge grounding, MCP tool-surface security, AI-asset inventory, policy-as-code, human-in-the-loop gating, tamper-evident (hash-chained, Ed25519-signed) audit logging |
| Zero Trust & Identity | Short-lived scoped service identities, attenuating delegation, cascade revocation, allow/deny/escalate policy enforcement, fail-closed design, conformance test matrices |
| Governance & Compliance | Enterprise governance frameworks (EAODS), controls & evidence automation, standard → control → implementation traceability, NIST CSF alignment |
| Detection Engineering | MITRE ATT&CK mapping, Sigma detection content & correlation rules, triage-to-detection feedback loop |
| Secure SDLC / DevSecOps | CI security gates (bandit, gitleaks, pip-audit, ruff, mypy --strict, CodeQL), 85% coverage gates, SBOM + checksummed releases, threat-model-driven specs & ADRs |
| Risk Management | Asset inventory, risk scoring, controls gap analysis, NIST CSF alignment |
| Network Security | VLAN segmentation, firewall policy, IDS/IPS (Suricata), DNS security |
| Traffic Analysis | Packet capture review, protocol analysis, IoC identification (Wireshark/tcpdump) |
| Incident Response | Timeline reconstruction, root-cause analysis, documentation |
| System Hardening | Linux file permissions, least privilege, SQL-based log investigation |
| Documentation | Executive summaries, case studies, structured reports, client-ready deliverables |

---

## Tools & Technologies

`Python` · `MITRE ATT&CK` · `Sigma` · `MCP` · `Zero Trust` · `Ed25519` ·
`RAG / Ollama / Qdrant` · `Streamlit` · `bandit` · `gitleaks` · `pip-audit` · `mypy` ·
`ruff` · `CodeQL` · `SARIF` · `MkDocs` · `Wireshark` · `tcpdump` · `Suricata` ·
`pfSense` · `UniFi` · `pfBlockerNG` · `Unbound DNS` · `Linux` · `SQL` · `Bash` ·
`NIST CSF` · `NIST SP 800-series` · `Jython`

---

## Contact

**Ivan Rozenblad**
- GitHub: [@IRsoctierDT](https://github.com/IRsoctierDT)
- Email: irozenblad@icloud.com

---

*This portfolio is for educational and professional demonstration purposes. All analysis was performed in controlled lab environments or on training datasets. Security tooling referenced here is for defensive, authorized use only.*
