# Ivan Rozenblad — Cybersecurity Portfolio

A working portfolio of hands-on cybersecurity projects spanning risk assessment, security auditing, network traffic analysis, incident response, and privacy/compliance. The artifacts here demonstrate practical application of security frameworks (NIST CSF, NIST SP 800-series), threat analysis, and defensive engineering.

> **Focus areas:** Security analysis · Risk & audit · Network defense · Incident response

---

## About Me

I'm a cybersecurity practitioner and technology consultant with hands-on experience in network engineering, security operations, and secure systems design. My work centers on defense-in-depth, least-privilege design, network segmentation, and auditable, well-documented security controls. I operate a home security lab built on pfSense (Netgate 4200), UniFi infrastructure, VLAN segmentation, Suricata IDS/IPS, pfBlockerNG, and Unbound DNS.

**Career direction:** Security Engineer · SOC Analyst · Penetration Tester

See my full [Professional Statement](./Professional%20Statement%20/Professional%20Statement.md).

---

## Projects

### Security Risk Assessment & Audit
- **`Audit-Scope-and-Goals.docx`** — Definition of audit scope, goals, and boundaries aligned to the NIST Cybersecurity Framework.
- **`Botium-Toys-Scope-goals-and-risk-assessment-report.docx`** — Full internal security risk assessment for a sample organization (Botium Toys): asset inventory, risk scoring, controls gap analysis, and remediation recommendations.
- **`Security-risk-assessment-report.docx`** — Structured security risk assessment report documenting threats, vulnerabilities, likelihood/impact, and prioritized mitigations.

### Network Traffic Analysis & Incident Response
- **[`Network_security_analysis.md`](./Network_security_analysis.md)** — Markdown writeup of a DNS/ICMP outage reconstructed from a packet capture: summary, packet-level data analysis, root cause, and remediation.
- **`21capture.pcapng`** — Raw packet capture used for protocol and traffic analysis (open with Wireshark/tshark).
- **`Cybersecurity incident report network traffic analysis.pdf`** / **`Cybersecurity-incident-report-network-traffic-analysis.docx`** — Incident analysis report reconstructing an event from captured network traffic, including timeline, indicators, root cause, and response actions.
- **`Cybersecurity_Incident_Report.docx`** — DNS/ICMP incident report analyzing a failed DNS resolution: a workstation's UDP query to port 53 returned an ICMP "Destination Unreachable – Port Unreachable," halting name resolution. Documents the problem summary, packet-level data analysis, root cause, and remediation.

### Linux & SQL Security Labs
- **[`Linux_permissions_lab.md`](./Linux_permissions_lab.md)** — Auditing and correcting Linux file permissions in a multi-user research directory, applying least privilege with `chmod`.
- **[`Secure_query_lab.md`](./Secure_query_lab.md)** — Investigating suspicious authentication activity with SQL filters across login and employee tables.

### Network Hardening
- **`Network-hardening-tools.xlsx`** — Catalog of network-hardening techniques and tools mapped to the controls they enforce (segmentation, firewall rules, access control, monitoring).

---

## Skills Demonstrated

| Domain | Highlights |
|---|---|
| Risk Management | Asset inventory, risk scoring, controls gap analysis, NIST CSF alignment |
| Network Security | VLAN segmentation, firewall policy, IDS/IPS (Suricata), DNS security |
| Traffic Analysis | Packet capture review, protocol analysis, IoC identification (Wireshark/tcpdump) |
| Incident Response | Timeline reconstruction, root-cause analysis, documentation |
| System Hardening | Linux file permissions, least privilege, SQL-based log investigation |
| Documentation | Executive summaries, structured reports, professional client-ready deliverables |

---

## Tools & Technologies

`Wireshark` · `tcpdump` · `Suricata` · `pfSense` · `UniFi` · `pfBlockerNG` · `Unbound DNS` · `Linux` · `SQL` · `NIST CSF` · `NIST SP 800-series` · `Python` · `Bash`

---

## How to Use This Repository

Most reports are provided as `.docx` / `.pdf`. The packet capture (`.pcapng`) can be opened in Wireshark, or inspected from the command line:

```bash
# Quick protocol summary
tshark -r 21capture.pcapng -q -z io,phs

# Top conversations
tshark -r 21capture.pcapng -q -z conv,ip
```

---

## Contact

**Ivan Rozenblad**
- GitHub: [@IRsoctierDT](https://github.com/IRsoctierDT)
- Email: irozenblad@icloud.com

---

*This portfolio is for educational and professional demonstration purposes. All analysis was performed in controlled lab environments or on training datasets.*
