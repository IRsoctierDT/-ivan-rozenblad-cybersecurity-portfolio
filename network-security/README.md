# Network Security

Network defense and traffic-analysis work — protocol analysis, packet capture review, and
network hardening.

| Artifact | Description |
|---|---|
| [`network-security-analysis.md`](./network-security-analysis.md) | DNS/ICMP outage analysis reconstructed from a packet capture: summary, data analysis, root cause, and remediation. |
| `dns-outage-capture.pcapng` | Raw packet capture for the DNS/ICMP incident (open with Wireshark/tshark). |
| `network-hardening-tools.xlsx` | Catalog of network-hardening techniques and tools mapped to the controls they enforce (segmentation, firewall rules, access control, monitoring). |

## Inspecting the capture

```bash
# Quick protocol summary
tshark -r dns-outage-capture.pcapng -q -z io,phs

# Top conversations
tshark -r dns-outage-capture.pcapng -q -z conv,ip
```

> **Related:** formal incident reports for this event are in
> [`../incident-response/`](../incident-response/).
