# Security Automation

**Status:** ✅ Active — flagship work lives in the [AI Operator Cyber Command Center](../projects/ai-operator-cyber-command-center.md).

This domain covers automation that reduces manual SOC effort: agentic log triage,
detection matching, enrichment, and report generation — always with a human approving
anything irreversible.

## Current artifacts

- **[AI Operator Cyber Command Center](../projects/ai-operator-cyber-command-center.md)** —
  local-first SOC automation platform: SOC analyst triage agent (0–100 severity scoring),
  detection matcher with lab-scoped Sigma content, multi-agent orchestration, policy-gated
  MCP tool surface, and an Ed25519-signed tamper-evident audit log. Ten case studies with
  reproducible worked examples.
- **[AI Agentic MCPscan](../projects/ai-agentic-mcpscan.md)** — published CLI scanner
  (PyPI) that automates security posture assessment of MCP/AI-agent setups, with a
  `--fail-on` severity gate for CI pipelines.

## Next

- Standalone log parsing / enrichment scripts extracted as portfolio artifacts
- Alert triage and notification automation for the home lab (Suricata → triage pipeline)
