# Network Security Analysis — DNS/ICMP Outage

**Author:** Ivan Rozenblad
**Type:** Network traffic analysis / incident writeup
**Tools:** tcpdump, Wireshark
**Companion capture:** `21capture.pcapng`

---

## Executive Summary

Users reported that a client website was unreachable, returning "destination port
unreachable" errors. Packet analysis showed that DNS queries sent over UDP to the
authoritative DNS server were never answered — each query was immediately met with an
ICMP **Destination Unreachable – Port Unreachable** (Type 3, Code 3) reply. The DNS
service on UDP port 53 was not listening, so name resolution failed for every dependent
client and the site became inaccessible. The root cause was a down or misconfigured DNS
service, not a network-path or client-side fault.

---

## Part 1: Summary of the Problem

During analysis of DNS and ICMP traffic, I observed that the workstation
(`192.51.100.15`) sent a DNS query over UDP to the DNS server (`203.0.113.2`) on port 53
while attempting to resolve `www.yummyrecipesforme.com`. The request carried query ID
`35084` and sought an **A record**, which maps a domain name to an IPv4 address.

Instead of a valid DNS response, the workstation received an ICMP **"Destination
Unreachable – Port Unreachable"** message from `203.0.113.2`. The message specifically
stated *"udp port 53 unreachable,"* meaning the DNS request never reached an active
service on that port.

Because port 53 is reserved for DNS operations, this error indicates the DNS service on
the destination server was not listening on UDP. Without DNS resolution, the browser
could not locate the web server, producing the "destination port unreachable" error for
users trying to reach the site.

**In short:** DNS requests over UDP failed because the server was not responding on
port 53, halting all name resolution for the domain.

---

## Part 2: Data Analysis and Cause of the Incident

**Time of incident:** The first failure occurred at `13:24:32.192571`, as shown in the
tcpdump capture.

**How the issue came to light:** Customers began reporting that they could not access the
client's website and received "destination port unreachable" errors. When the IT team
attempted to replicate the issue, the same error appeared.

**Investigation process:** The team used `tcpdump` to monitor network traffic during an
attempt to load the site. The capture confirmed that DNS queries were being sent from the
workstation to `203.0.113.2`, but every query was immediately followed by an ICMP
**Type 3, Code 3** response — the "port unreachable" message. The pattern repeated across
multiple attempts, confirming the issue was persistent rather than intermittent.

### Key Findings

| Field | Value |
|---|---|
| Source IP | `192.51.100.15` |
| Destination IP | `203.0.113.2` |
| Protocol | UDP (DNS service) |
| Affected port | `53` (DNS) |
| Error | ICMP Destination Unreachable – Port Unreachable (Type 3, Code 3) |
| Domain queried | `www.yummyrecipesforme.com` |
| Query ID | `35084` (A record) |

All indicators pointed to a DNS outage or configuration issue. Because the ICMP responses
indicated the port itself was closed, the server likely had its DNS daemon stopped,
misconfigured, or blocked by a host firewall.

### Probable Cause

The DNS service on `203.0.113.2` was **down or misconfigured**, leaving UDP port 53
closed. This caused DNS lookups to fail for all dependent clients. Without successful name
resolution, browsers could not connect to the web server over HTTPS, producing the outage
reported by users.

---

## Recommended Remediation

1. **Restore the DNS service** — confirm the DNS daemon (e.g., BIND/`named`) is running on
   `203.0.113.2` and bound to UDP/TCP port 53; restart and re-test resolution.
2. **Verify host firewall rules** — ensure UDP/53 and TCP/53 are permitted to the DNS
   service so legitimate queries are not silently dropped.
3. **Add service monitoring** — alert on DNS daemon availability and on spikes in ICMP
   Type 3/Code 3 responses so the next outage is detected before users report it.
4. **Provision redundancy** — configure a secondary/resolver DNS server so a single
   service failure does not halt name resolution for all clients.
5. **Document and review** — capture this incident in the response log and review DNS
   change-management to prevent a recurrence.

---

*Analysis performed on a training dataset in a controlled lab environment. IP addresses
and domains shown are from documentation/training ranges (RFC 5737 / example domains).*
