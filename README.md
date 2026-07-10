# Ivan Rozenblad — Cybersecurity Portfolio

A working portfolio of hands-on cybersecurity projects spanning AI-driven security
automation, risk assessment, security auditing, network traffic analysis, incident
response, and security tooling. The artifacts here demonstrate practical application of
security frameworks (NIST CSF, NIST SP 800-series, MITRE ATT&CK), threat analysis, and
defensive engineering.

> **Focus areas:** AI × defensive security · Security automation · Risk & audit · Network defense · Incident response

---

## About Me

I'm a cybersecurity practitioner and technology consultant with hands-on experience in
network engineering, security operations, and secure systems design. My work centers on
defense-in-depth, least-privilege design, network segmentation, and auditable,
well-documented security controls. I operate a home security lab built on pfSense
(Netgate 4200), UniFi infrastructure, VLAN segmentation, Suricata IDS/IPS, pfBlockerNG,
and Unbound DNS.

My current focus is the **intersection of AI and defensive security**: building agentic
SOC automation (triage, MITRE mapping, RAG-grounded incident reporting) and securing the
AI-agent ecosystem itself with [MCPscan](./projects/ai-agentic-mcpscan.md), an
open-source posture scanner published on PyPI.

**Career direction:** Security Engineer · SOC / Detection Engineer · AI Security Engineer

See my full [Professional Statement](./professional-statement.md).

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
