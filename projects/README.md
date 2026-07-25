# Active Projects

Flagship engineering projects that live in their own repositories. Each page here is a
portfolio artifact summarizing what the project is, what's built, and what it demonstrates —
with links into the source, documentation, and case studies.

Most of this work now ships under the **IANUA** umbrella (Latin for "gateway"): a
platform (IANUA), a scanner (IANUA-Broker), a zero-trust identity layer (Agent Trust
Broker), and the governance framework that binds them (EAODS).

| Project | Repo | Status | One-liner |
|---|---|---|---|
| [IANUA — AI Operations & Cyber Command Center](./ianua.md) | [source](https://github.com/IRsoctierDT/IANUA) | Active — all agents built; zero-trust + compliance layers landing | Local-first SOC automation platform: agentic triage, MITRE mapping, RAG, policy-gated MCP tools, signed audit log, compliance layer, 11 case studies |
| [IANUA-Broker — AI Agentic MCPscan](./ianua-broker-mcpscan.md) | [source](https://github.com/IRsoctierDT/IANUA-Broker) · [PyPI](https://pypi.org/project/ai-agentic-mcpscan/) | **Stable v1.x** (v1.4.0) on PyPI | Offline-by-default posture scanner + AI-asset inventory for MCP/agent setups: 7 host adapters, SARIF code scanning, opt-in `--fix`, gated LAN scanning |
| [Agent Trust Broker](./agent-trust-broker.md) | [source](https://github.com/IRsoctierDT/agent-trust-broker) | Active — v0.1 reference implementation | Zero-trust identity + policy enforcement for AI-agent fleets: short-lived scoped identities, allow/deny/escalate, hash-chained audit, fail-closed |
| [EAODS — Enterprise AI Operator Documentation Suite](./eaods.md) | [source](https://github.com/IRsoctierDT/EAODS-v3) | Active — release line v17.0–v17.3 | Enterprise governance framework for AI-assisted organizations; its patterns are reference-implemented by ATB and enforced inside IANUA |
| [AppSec Supply Chain Lab](./appsec-supply-chain-lab.md) | [repo](https://github.com/IRsoctierDT/portfolio-appsec-lab) | 🚧 In progress | Lab for detecting & remediating software supply chain vulnerabilities across ecosystems |

**Why these projects:** my focus is the intersection of AI and defensive security —
using agentic automation to scale SOC work, securing the AI-agent ecosystem itself, and
building the governance layer that makes autonomous operations trustworthy. See the
[Professional Statement](../professional-statement.md) for the full picture.
