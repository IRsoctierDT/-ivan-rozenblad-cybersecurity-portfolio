# IANUA Agent Trust Broker (ATB)

**Repo:** [IRsoctierDT/agent-trust-broker](https://github.com/IRsoctierDT/agent-trust-broker)
**Stack:** Python (stdlib only) · CLI (`atb`)
**Status:** Active — v0.1 design volumes and reference implementation built; wired into IANUA's MCP tool dispatch

---

## What it is

**Identity issuance and Zero-Trust policy enforcement for an AI-agent fleet.** Every
privileged agent action requires a verifiable, short-lived, scoped identity and a
per-action **allow / deny / escalate** decision, recorded in a hash-chained audit log —
**fail-closed by construction**.

ATB is the reference implementation of [EAODS](./eaods.md) **PAT-0001 (Zero Trust
Service Identity)** and **EAODS-CTRL-000184 (Service Identity Verification)**, and the
mitigation architecture for threat models THR-0001 and THR-0002. It answers the question
the AI-agent industry is only starting to ask: *when an autonomous agent calls a
privileged tool, who is it, what exactly is it allowed to do, and who said so?*

## What's built

| Module | Responsibility |
|---|---|
| `atb.catalog` | Closed-world scope catalog; escalation flags; static validation |
| `atb.bindings` | Least-privilege role → scope bindings, validated at import |
| `atb.identity` | Mint / verify / revoke; depth-1 attenuating delegation; cascade revocation |
| `atb.policy` | Deterministic authorize → allow / deny / escalate; always audited |
| `atb.audit` | Append-only, hash-chained decision log with chain verification |
| `atb.persistence` | Durable JSONL audit storage; chain re-verified fail-closed on load |
| `atb.escalation` | Persistent escalation queue; human approve/deny recorded in the chain |
| `atb.cli` | Operator CLI: `atb pending / approve / deny / verify` |

Two design volumes (ATB-01: identity, policy, escalation, audit model; ATB-02: scope
catalog, delegation model, conformance matrix) document the architecture before the code.

## Security engineering demonstrated

- **Zero-trust for machine identities** — short-lived, scoped, verifiable credentials
  with attenuating delegation (a delegated identity can only ever hold a subset of its
  parent's scopes) and cascade revocation.
- **Fail-closed everywhere** — tampered or missing audit chains, unknown references, and
  double resolutions all deny and exit non-zero; signing keys are injected at
  construction, never hard-coded, never logged.
- **Conformance as tests** — the ATB-02 **T1–T12 trust-boundary matrix** is implemented
  one-to-one in `tests/security/test_conformance.py`: each test asserts a denial, an
  escalation, or chain integrity.
- **Human-in-the-loop escalation** — approvals are one-shot, triple-bound, attributed to
  a named approver, require a written reason, and are recorded in the same hash chain
  they authorize.
- **Zero dependencies** — stdlib only, so the trust component itself adds no supply
  chain surface.

## In production use

IANUA's MCP server routes **every tool dispatch** through an ATB gate — see the
[Agent Trust Broker Gate case study](https://github.com/IRsoctierDT/IANUA/blob/main/docs/case-studies/agent-trust-broker-gate.md)
in the IANUA repo.
