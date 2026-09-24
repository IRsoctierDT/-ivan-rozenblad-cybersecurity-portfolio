# Professional Statement — Ivan Rozenblad

**Emeryville, CA** · [GitHub @IRsoctierDT](https://github.com/IRsoctierDT) · irozenblad@icloud.com  
**Targets:** Security Engineer · Detection / SOC Engineer · AI Security Engineer · selective consulting

## Who I am

I am a cybersecurity practitioner and technology consultant in the San Francisco Bay Area. I came to security through operating real networks and systems — not through a purely academic path — and that still shapes how I build: controls have to be practical, auditable, and maintainable, or they do not survive production.

## Philosophy

1. **Defense in depth, least privilege by default.** Design as if a layer will fail. Segment, allow-list, default-deny.
2. **If it is not documented and testable, it is not a control.** Threat models, decision records, CI security gates, reproducible evidence.
3. **Humans approve; machines assist.** Automation may recommend, draft, classify, and prioritize. People authorize irreversible or high-impact actions.

## What I am building now (Sep 2026)

Flagship work ships under the **IANUA** ecosystem — platform, scanner, identity layer, and governance framework:

- **[IANUA](https://github.com/IRsoctierDT/IANUA)** — local-first AI operations / cyber command center: agentic triage, MITRE ATT&CK mapping, RAG, policy-gated tools, tamper-evident audit, compliance/trust surfaces, reproducible case studies. Docs: [irsoctierdt.github.io/IANUA](https://irsoctierdt.github.io/IANUA/).
- **[IANUA-Broker](https://github.com/IRsoctierDT/IANUA-Broker)** — offline-by-default MCP / local-agent posture scanner (`mcpscan`), published on PyPI as [`ianua-broker`](https://pypi.org/project/ianua-broker/) (v1.5.2 line). Docs: [irsoctierdt.github.io/IANUA-Broker](https://irsoctierdt.github.io/IANUA-Broker/).
- **[Agent Trust Broker](https://github.com/IRsoctierDT/agent-trust-broker)** — zero-trust agent identity, scoped short-lived credentials, allow/deny/escalate policy, hash-chained audit; fail-closed reference implementation for privileged tool dispatch.
- **[EAODS v3 Enterprise](https://github.com/IRsoctierDT/EAODS-v3-Enterprise-Edition)** — enterprise AI operator documentation / governance / cyber-defense suite with schema validation and CI gates; patterns implement in ATB → IANUA. Docs site live on GitHub Pages.
- **AppSec supply-chain lab** — dependency and SBOM-oriented detection / remediation practice environment (in progress).
- **Brotherhood Accountability** (private) — local-first covenant accountability product with passkeys, witnessed commitments, and Cloudflare-backed sync; App Store packaging via Capacitor in progress.

I still train the fundamentals in public artifacts: Wireshark/pcap IR writeups, NIST CSF-aligned risk assessments, Linux hardening labs, and home-lab detection work (pfSense / UniFi / Suricata-class stacks).

## Direction

I want a security engineering seat where I own defensive tooling and automation — especially detection engineering and AI-security controls — or consulting engagements with the same bar. Near-term focus:

- Grow real-world adoption of `ianua-broker` / mcpscan while MCP ecosystems move underfoot
- Mature Agent Trust Broker toward a default pattern for scoped agent authority
- Deepen Sigma/detection content and triage→detection feedback inside IANUA
- Finish the supply-chain lab as a portfolio-grade artifact set
- Keep governance (EAODS) honest: standard → control → implementation → test

## Contact

**Ivan Rozenblad** · Emeryville, CA  
GitHub: [@IRsoctierDT](https://github.com/IRsoctierDT) · Email: irozenblad@icloud.com  
Portfolio: https://irsoctierdt.github.io/-ivan-rozenblad-cybersecurity-portfolio/
