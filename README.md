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
  [AI Agentic MCPscan](./projects/ai-agentic-mcpscan.md) is live on
  [PyPI](https://pypi.org/project/ai-agentic-mcpscan/) with SBOM'd, checksummed releases
  behind a cross-platform CI gate, and the
  [AI Operator Cyber Command Center](./projects/ai-operator-cyber-command-center.md) is
  a fully built SOC automation platform documented in ten reproducible case studies.
- **I work both sides of the AI/security boundary.** Using AI to scale defense —
  agentic log triage, MITRE ATT&CK mapping, RAG-grounded incident reporting — and
  securing the AI-agent ecosystem itself: MCP posture scanning, policy-gated tool
  surfaces, and tamper-evident (hash-chained, Ed25519-signed) audit logging.
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

| Project | Status | What it demonstrates |
|---|---|---|
| [AI Operator Cyber Command Center](./projects/ai-operator-cyber-command-center.md) | Active — all 8 agent blueprints built | Local-first SOC automation: agentic triage (0–100 severity), MITRE ATT&CK mapping, threat-intel enrichment, RAG pipeline, policy-gated MCP tools, Ed25519-signed tamper-evident audit log, Sigma detections, Streamlit dashboard. Ten reproducible case studies. |
| [AI Agentic MCPscan](./projects/ai-agentic-mcpscan.md) | Beta v0.3.0 — [on PyPI](https://pypi.org/project/ai-agentic-mcpscan/) | Offline-by-default posture scanner for MCP/AI-agent setups: finds exposed servers, plaintext secrets, over-broad tool scopes, unpinned packages; A–F grading; threat-model-driven spec, SBOM'd releases, cross-platform CI. |
| [AppSec Supply Chain Lab](./projects/appsec-supply-chain-lab.md) | 🚧 In progress | Detecting & remediating software supply chain vulnerabilities across package ecosystems. |

---

## Repository Structure

```
cybersecurity-portfolio/
├── README.md
├── professional-statement.md
├── projects/                   # Artifacts for flagship external repos
│   ├── ai-operator-cyber-command-center.md
│   ├── ai-agentic-mcpscan.md
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
| [projects](./projects/) | AI Operator Cyber Command Center, MCPscan, AppSec supply chain lab |
| [security-automation](./security-automation/) | Agentic SOC triage, Sigma detection loop, MCP posture scanning in CI |
| [threat-intelligence](./threat-intelligence/) | IOC triage agent, MITRE ATT&CK mapper (case studies) |
| [labs](./labs/) | SQL filtering, Linux permissions, Jython install & validation |
| [incident-response](./incident-response/) | DNS/ICMP outage and network-traffic incident reports |
| [network-security](./network-security/) | Packet-capture analysis writeup, `.pcapng` capture, hardening catalog |
| [risk-assessment](./risk-assessment/) | Botium Toys audit, audit scope & goals, risk assessment reports (NIST CSF) |
| [malware-analysis](./malware-analysis/) | 🚧 Planned |

---

## Skills Demonstrated

| Domain | Highlights |
|---|---|
| AI Security & Automation | Agentic SOC pipelines, RAG knowledge grounding, MCP tool-surface security, policy-as-code, human-in-the-loop gating, tamper-evident (hash-chained, Ed25519-signed) audit logging |
| Detection Engineering | MITRE ATT&CK mapping, Sigma detection content, triage-to-detection feedback loop |
| Secure SDLC / DevSecOps | CI security gates (bandit, gitleaks, pip-audit, ruff, mypy --strict), 85% coverage gates, SBOM + checksummed releases, threat-model-driven specs & ADRs |
| Risk Management | Asset inventory, risk scoring, controls gap analysis, NIST CSF alignment |
| Network Security | VLAN segmentation, firewall policy, IDS/IPS (Suricata), DNS security |
| Traffic Analysis | Packet capture review, protocol analysis, IoC identification (Wireshark/tcpdump) |
| Incident Response | Timeline reconstruction, root-cause analysis, documentation |
| System Hardening | Linux file permissions, least privilege, SQL-based log investigation |
| Documentation | Executive summaries, case studies, structured reports, client-ready deliverables |

---

## Tools & Technologies

`Python` · `MITRE ATT&CK` · `Sigma` · `MCP` · `RAG / Ollama / Qdrant` · `Streamlit` ·
`bandit` · `gitleaks` · `pip-audit` · `mypy` · `ruff` · `Wireshark` · `tcpdump` ·
`Suricata` · `pfSense` · `UniFi` · `pfBlockerNG` · `Unbound DNS` · `Linux` · `SQL` ·
`Bash` · `NIST CSF` · `NIST SP 800-series` · `Jython`

---

## Contact

**Ivan Rozenblad**
- GitHub: [@IRsoctierDT](https://github.com/IRsoctierDT)
- Email: irozenblad@icloud.com

---

*This portfolio is for educational and professional demonstration purposes. All analysis was performed in controlled lab environments or on training datasets. Security tooling referenced here is for defensive, authorized use only.*
