# EAODS — Enterprise AI Operator Documentation Suite

**Repo:** [IRsoctierDT/EAODS-v3](https://github.com/IRsoctierDT/EAODS-v3)
**Stack:** MkDocs documentation portal · versioned framework volumes · schema-validated front matter · CI quality gates
**Status:** Active — current release line **EAODS v17.0–v17.3**

---

## What it is

An **enterprise architecture, governance, cybersecurity, and operationalization
framework for governed AI-assisted organizations** — the standards layer that sits above
my engineering projects and defines how an organization runs AI operators safely:
threat models, patterns, controls, reference architectures, and operations playbooks.

## Current release line

| Volume | Contents |
|---|---|
| **EAODS v17.0** | Enterprise Cyber Defense & Digital Resilience Framework |
| **EAODS v17.1** | Domain 03 Reference Architecture and Implementation Blueprint |
| **EAODS v17.2** | Domain 03 Operations Manual and Executive Playbook |
| **EAODS v17.3** | Domain 03 Reference Implementation and Platform Engineering Guide |

## How it's governed

Every framework document requires YAML front matter, traceability, QA checks,
integration points, and a human review gate — enforced by schemas, templates, a
controlled vocabulary under `standards/`, ADRs under `architecture/`, and GitHub Actions
quality/publishing automation. The framework practices the governance it prescribes.

## From standard to running code

EAODS is not paperware — its patterns and controls trace directly into my running
systems:

- **PAT-0001 (Zero Trust Service Identity)** and **CTRL-000184 (Service Identity
  Verification)** are reference-implemented by the
  [Agent Trust Broker](./agent-trust-broker.md), which in turn gates every MCP tool
  dispatch inside [IANUA](./ianua.md).
- Threat models **THR-0001 / THR-0002** drive ATB's mitigation architecture and
  conformance test matrix.

That standard → control → implementation → conformance-test chain is the same
traceability discipline used in mature compliance programs (NIST CSF/800-53 style),
applied to the emerging problem of governing autonomous AI operators.
