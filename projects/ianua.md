# IANUA — AI Operations & Cyber Command Center

**Repo:** [IRsoctierDT/IANUA](https://github.com/IRsoctierDT/IANUA) *(formerly `ai-operator-cyber-command-center`)*
**Stack:** Python · Ollama (local LLM) · RAG (Qdrant / local embeddings) · MCP (stdio JSON-RPC) · Sigma · Streamlit
**Status:** Active — all agent blueprints built; current work: zero-trust identity enforcement and compliance automation

---

## What it is

**IANUA** (Latin for "gateway") is a **local-first, secure-by-default command center** for
AI-driven security operations: agentic log triage, MITRE ATT&CK mapping, threat-intel
enrichment, RAG-grounded incident reporting, and detection matching — designed around
one architectural rule:

> **Agents recommend, draft, classify, and structure. Humans approve anything
> destructive, external, legal, financial, or security-sensitive.**

Everything runs locally (loopback-only LLM, confined filesystem access), and every
component is documented, tested, and reviewable.

## What's built

| Component | What it does |
|---|---|
| **SOC Analyst Agent** | JSON/text log triage, 0–100 severity scoring, evidence table, MITRE mapping, incident report |
| **MITRE Mapper Agent** | Deterministic event → ATT&CK tactic/technique mapping with confidence scoring |
| **Threat Intel Agent** | IOC triage and enrichment — returns `unknown` + "enrich first" instead of guessing |
| **Vulnerability Assessment Agent** | Ranks authorized scan findings into a defensible remediation order |
| **Incident Report Agent** | Markdown incident reports from structured SOC + MITRE output |
| **Knowledge Base Agent** | Grounds reports in a cited cybersecurity corpus (NIST, MITRE, CIS, OWASP) |
| **Detection Matcher + Orchestrator** | Triage → Sigma detection loop with cross-referenced correlation rules; full multi-agent pipeline in one call |
| **RAG Pipeline** | Confined ingest → chunk → embed → cited retrieval; fully offline mode for air-gapped labs |
| **MCP Server** | Allow-listed, self-validating, path-confined, policy-gated tool surface — now with a **trust-broker identity gate on every tool dispatch** |
| **Policy Engine + Audit Log** | Default-deny policy-as-code; hash-chained, **Ed25519-signed tamper-evident audit trail** |
| **Compliance Layer** | Vanta-style controls mapping, evidence collection, and trust page |
| **Dashboard** | Streamlit command center: SOC workflow, batch processing, KB search, **pending-approvals escalation queue**, system health, reports |

## Security engineering demonstrated

- **Zero-trust agent identity** — every privileged tool dispatch passes through an
  [Agent Trust Broker](./agent-trust-broker.md) gate: verifiable, short-lived, scoped
  identities with per-action allow / deny / escalate decisions.
- **Governance-first development** — an `AGENTS.md` operating charter, written threat
  model and decision log (`DESIGN.md`), and CI gates: bandit, gitleaks, pip-audit, mypy,
  ruff, pytest with an 85% coverage requirement, least-privilege CI job permissions.
- **Tamper-evident auditability** — hash-chained audit log with asymmetric Ed25519
  signing via a pluggable signer.
- **Human-in-the-loop by design** — no agent can take an irreversible action;
  escalations land in a read-only Pending Approvals queue for human resolution.
- **Detection engineering** — lab-scoped Sigma detection content with correlation rules
  wired into a triage-to-detection feedback loop.
- **Compliance automation** — controls, evidence, and trust-page reporting built into
  the platform rather than bolted on.

## Artifacts to read

Eleven portfolio-grade case studies — each with a worked example (real command output)
and a reproduce-it-yourself section:
[docs/case-studies](https://github.com/IRsoctierDT/IANUA/tree/main/docs/case-studies)

Highlights:

- [SOC Analyst Agent v0.2](https://github.com/IRsoctierDT/IANUA/blob/main/docs/case-studies/soc-analyst-v0.2.md) — raw log line → triaged, MITRE-mapped, human-reviewable incident, fully local
- [Agent Trust Broker Gate](https://github.com/IRsoctierDT/IANUA/blob/main/docs/case-studies/agent-trust-broker-gate.md) — zero-trust identity enforcement on the MCP tool surface
- [Policy Engine & Tamper-Evident Audit Log](https://github.com/IRsoctierDT/IANUA/blob/main/docs/case-studies/policy-and-audit.md)
- [Policy-Gated MCP Tool Surface](https://github.com/IRsoctierDT/IANUA/blob/main/docs/case-studies/mcp-server.md)
- [Local RAG Pipeline](https://github.com/IRsoctierDT/IANUA/blob/main/docs/case-studies/rag-pipeline.md)
