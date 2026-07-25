# Security Automation

**Status:** ✅ Active — flagship work lives in [IANUA](../projects/ianua.md), the AI operations & cyber command center.

This domain covers automation that reduces manual SOC effort: agentic log triage,
detection matching, enrichment, and report generation — always with a human approving
anything irreversible.

## Current artifacts

- **[IANUA](../projects/ianua.md)** — local-first SOC automation platform: SOC analyst
  triage agent (0–100 severity scoring), detection matcher with Sigma correlation rules,
  multi-agent orchestration, a policy-gated MCP tool surface with a zero-trust
  identity gate on every dispatch, an Ed25519-signed tamper-evident audit log, and a
  Vanta-style compliance layer. Eleven case studies with reproducible worked examples.
- **[IANUA-Broker / MCPscan](../projects/ianua-broker-mcpscan.md)** — stable v1.x CLI
  scanner (PyPI) that automates security posture assessment and AI-asset inventory for
  MCP/agent setups, with SARIF output and a `--fail-on` severity gate for CI pipelines.
- **[Agent Trust Broker](../projects/agent-trust-broker.md)** — zero-trust identity and
  policy enforcement for agent fleets: automated allow/deny/escalate decisions on every
  privileged action, with a human escalation queue and hash-chained audit.

## Next

- Standalone log parsing / enrichment scripts extracted as portfolio artifacts
- Alert triage and notification automation for the home lab (Suricata → triage pipeline)
