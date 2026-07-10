# Threat Intelligence

**Status:** ✅ Active — first artifacts shipped inside the [AI Operator Cyber Command Center](../projects/ai-operator-cyber-command-center.md).

This domain holds threat-intelligence work: IOC research and enrichment, threat-actor
and TTP profiling (MITRE ATT&CK mapping), and analysis that informs detection and
defense.

## Current artifacts

- **[Threat Intelligence Agent — case study](https://github.com/IRsoctierDT/ai-operator-cyber-command-center/blob/main/docs/case-studies/threat-intel-agent.md)** —
  indicator triage that deliberately returns `unknown` + "enrich first" instead of
  guessing; IOC enrichment and indicator summarization.
- **[MITRE ATT&CK Mapper Agent — case study](https://github.com/IRsoctierDT/ai-operator-cyber-command-center/blob/main/docs/case-studies/mitre-mapper-agent.md)** —
  deterministic event → tactic/technique mapping with confidence scoring and evidence.

## Next

- Standalone IOC enrichment writeups from home-lab Suricata/pfBlockerNG telemetry
- Threat-actor / campaign profiles
