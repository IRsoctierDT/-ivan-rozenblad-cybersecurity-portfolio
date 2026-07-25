# Professional Statement — Ivan Rozenblad

## Who I Am

I'm a cybersecurity practitioner and technology consultant based in the San Francisco Bay Area, with hands-on experience in network engineering, security operations, and secure systems design. I came to security through building and operating real infrastructure — networks, servers, and the tooling that keeps them observable and defensible — and that operator's perspective shapes everything I build: security controls have to be practical, auditable, and maintainable, or they don't survive contact with production.

## My Security Philosophy

Three principles run through all of my work:

1. **Defense in depth, least privilege by default.** Every system I design assumes a layer will fail. Segmentation, allow-listing, and default-deny policy are the baseline, not the aspiration.
2. **If it isn't documented and testable, it isn't a control.** I hold my own projects to the same standard I'd apply in an audit: written threat models, decision records, CI quality gates, and reproducible results.
3. **Humans approve, machines assist.** As I build increasingly automated and AI-driven security tooling, I keep a hard architectural rule: automation recommends, drafts, classifies, and prioritizes — humans approve anything irreversible, destructive, or security-sensitive.

## What I'm Building Right Now

My current focus is the intersection of **AI and defensive security** — both using AI to scale security operations, and securing the AI-agent ecosystems that organizations are now rapidly adopting.

My flagship work now ships as the **IANUA ecosystem** — a platform, a scanner, a
zero-trust identity layer, and the governance framework that binds them:

- **[IANUA](https://github.com/IRsoctierDT/IANUA)** — a local-first, secure-by-default AI operations & cyber command center. It runs a fleet of specialized agents (SOC analyst triage with 0–100 severity scoring, MITRE ATT&CK mapping, threat-intel enrichment, vulnerability assessment ranking, incident reporting) over a local RAG knowledge base, behind a policy-gated MCP tool surface with a zero-trust identity gate on every dispatch, a tamper-evident Ed25519-signed audit log, Sigma correlation rules, and a Vanta-style compliance layer (controls, evidence, trust page). Eleven case studies document each component end-to-end.
- **[IANUA-Broker / AI Agentic MCPscan](https://github.com/IRsoctierDT/IANUA-Broker)** — an open-source (Apache-2.0), offline-by-default security posture scanner for MCP servers and local AI-agent setups, published on PyPI as `ai-agentic-mcpscan` and now **stable v1.x** (v1.4.0). It inventories a machine's AI infrastructure as typed assets, finds exposed servers, plaintext secrets, over-broad tool scopes, and unpinned packages across seven agent ecosystems (Claude, Cursor, Windsurf, Cline, VS Code, Zed, Continue), grades posture A–F, emits SARIF 2.1.0 for GitHub code scanning, offers a safe opt-in `--fix`, and supports authorized LAN scanning behind an explicit policy gate.
- **[Agent Trust Broker](https://github.com/IRsoctierDT/agent-trust-broker)** — zero-trust identity issuance and policy enforcement for AI-agent fleets: every privileged action requires a verifiable, short-lived, scoped identity and a per-action allow / deny / escalate decision recorded in a hash-chained audit log, fail-closed by construction, with a T1–T12 conformance test matrix and a human-operator escalation CLI. It gates every tool dispatch inside IANUA.
- **[EAODS](https://github.com/IRsoctierDT/EAODS-v3)** — the Enterprise AI Operator Documentation Suite (release line v17.0–v17.3): an enterprise architecture, governance, and cyber-defense framework for AI-assisted organizations, with schema-validated documents, traceability, and CI quality gates. Its zero-trust identity pattern (PAT-0001) is reference-implemented by the Agent Trust Broker — a complete standard → control → implementation → conformance-test chain.
- **[Application Security Lab](https://github.com/IRsoctierDT/portfolio-appsec-lab)** — an in-progress lab environment for detecting and remediating software supply chain vulnerabilities across multiple package ecosystems.
- **Home security lab** — a continuously evolving defensive environment built on pfSense (Netgate 4200), UniFi infrastructure, VLAN segmentation, Suricata IDS/IPS, pfBlockerNG, and Unbound DNS, where I test detection rules, hardening changes, and network policy before writing about them.

Alongside the building, I maintain the foundations: traffic analysis in Wireshark, incident response documentation, NIST CSF-aligned risk assessment and auditing, Linux hardening, and SQL-based log investigation — all captured as artifacts in this portfolio. I also work continuously on secure coding practice (including GitHub's Secure Code Game) and treat every project's CI pipeline as a security exercise: bandit, gitleaks, pip-audit, mypy --strict, SBOM generation, and signed releases are standard equipment in my repositories.

## Where I'm Headed

My goal is a security engineering role where I can own defensive tooling and automation — **security engineer, SOC/detection engineer, or AI security engineer**. Specifically, I want to:

- **Grow MCPscan's adoption in the stable v1.x line** — 1.0 shipped with the full planned feature set and the line keeps moving (AI-asset inventory, CodeQL, dependency hardening); the goal now is real-world dogfooding, community adoption, and keeping pace with the fast-moving MCP ecosystem — a trusted tool for the AI-agent security niche while the industry still lacks one.
- **Make zero-trust agent identity the norm** — mature the Agent Trust Broker from v0.1 reference implementation toward the standard way an agent fleet proves who is acting, under what scope, on whose authority — and keep EAODS evolving as the governance framework those controls trace back to.
- **Deepen detection engineering** — expand IANUA's Sigma correlation content and triage-to-detection feedback loop, and bring that discipline to a production SOC.
- **Build out the AppSec supply chain lab** into a full artifact set: dependency-confusion and typosquatting detection, SBOM-driven vulnerability management, and remediation playbooks.
- **Keep raising the governance bar** — I believe the security engineers who thrive in the next decade will be the ones who can direct AI systems safely: with policy-as-code, audit trails, and human-in-the-loop gates. I'm building that muscle now, in public, in my repositories — and writing the framework (EAODS) that makes it repeatable for others.

Protecting systems and data isn't abstract to me — it's the craft of making complex infrastructure legible, governable, and resilient. That's the work I want to do, and this portfolio is the evidence of how I do it.

---

**Ivan Rozenblad** · Emeryville, CA · [GitHub @IRsoctierDT](https://github.com/IRsoctierDT) · irozenblad@icloud.com
