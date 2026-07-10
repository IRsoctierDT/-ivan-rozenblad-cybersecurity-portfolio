# AI Operator Cyber Command Center

**Repo:** [IRsoctierDT/ai-operator-cyber-command-center](https://github.com/IRsoctierDT/ai-operator-cyber-command-center)
**Stack:** Python · Ollama (local LLM) · RAG (Qdrant / local embeddings) · MCP (stdio JSON-RPC) · Sigma · Streamlit
**Status:** Active — all eight agent blueprints built; current work is defense-in-depth hardening

---

## What it is

A **local-first, secure-by-default command center** for AI-driven security operations:
agentic log triage, MITRE ATT&CK mapping, threat-intel enrichment, RAG-grounded incident
reporting, and detection matching — designed around one architectural rule:

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
| **Detection Matcher + Orchestrator** | Triage → Sigma detection loop; full multi-agent pipeline in one call |
| **RAG Pipeline** | Confined ingest → chunk → embed → cited retrieval; fully offline mode for air-gapped labs |
| **MCP Server** | Allow-listed, self-validating, path-confined, policy-gated tool surface |
| **Policy Engine + Audit Log** | Default-deny policy-as-code; hash-chained, **Ed25519-signed tamper-evident audit trail** |
| **Dashboard** | Streamlit command center: SOC workflow, batch processing, KB search, system health, reports |

## Security engineering demonstrated

- **Governance-first development** — an `AGENTS.md` operating charter, written threat
  model and decision log (`DESIGN.md`), and CI gates: bandit, gitleaks, pip-audit, mypy,
  ruff, pytest with an 85% coverage requirement, least-privilege CI job permissions.
- **Tamper-evident auditability** — hash-chained audit log with asymmetric Ed25519
  signing via a pluggable signer.
- **Human-in-the-loop by design** — no agent can take an irreversible action; policy
  gates are default-deny.
- **Detection engineering** — lab-scoped Sigma detection content wired into a
  triage-to-detection feedback loop.

## Artifacts to read

Ten portfolio-grade case studies — one per component, each with a worked example (real
command output) and a reproduce-it-yourself section:
[docs/case-studies](https://github.com/IRsoctierDT/ai-operator-cyber-command-center/tree/main/docs/case-studies)

Highlights:

- [SOC Analyst Agent v0.2](https://github.com/IRsoctierDT/ai-operator-cyber-command-center/blob/main/docs/case-studies/soc-analyst-v0.2.md) — raw log line → triaged, MITRE-mapped, human-reviewable incident, fully local
- [Policy Engine & Tamper-Evident Audit Log](https://github.com/IRsoctierDT/ai-operator-cyber-command-center/blob/main/docs/case-studies/policy-and-audit.md)
- [Policy-Gated MCP Tool Surface](https://github.com/IRsoctierDT/ai-operator-cyber-command-center/blob/main/docs/case-studies/mcp-server.md)
- [Local RAG Pipeline](https://github.com/IRsoctierDT/ai-operator-cyber-command-center/blob/main/docs/case-studies/rag-pipeline.md)
