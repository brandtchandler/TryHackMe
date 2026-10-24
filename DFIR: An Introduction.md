# TryHackMe — DFIR: An Introduction

**Platform**: TryHackMe  
**Difficulty**: Easy  
**Category**: Digital Forensics & Incident Response  
**Date**: —  
**Time spent**: —  
**Tags**: `#DigitalForensics` `#IncidentResponse` `#EvidencePreservation` `#ChainofCustody` `#PICERL` `#NISTSP800-61` `#Forensics`

First module in the Digital Forensics and Incident Response learning path. Foundational entry point that builds on general defensive concepts (Pre-Security / Introduction to Cyber Security) and introduces the structured process of investigating and responding to a breach.

## Overview

Shifts from broad defensive ideas into the practical discipline of DFIR. The core security throughline is the order of volatility and chain of custody — the principles that underpin every forensic collection, evidence handling decision, and timeline reconstruction in later rooms.

## Learning Objectives

- Introduce DFIR and why it exists
- Cover foundational concepts used throughout the field
- Walk through the industry-standard Incident Response process
- Survey the main tools used in DFIR work

## Task Index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Sets the stage and learning objectives |
| 2 | The Need for DFIR | Defines DFIR, why it matters, and who performs it |
| 3 | Basic Concepts | Artifacts, evidence preservation, chain of custody, order of volatility, timeline creation |
| 4 | DFIR Tools | Eric Zimmerman’s tools, KAPE, Autopsy, Volatility, Redline, Velociraptor |
| 5 | Incident Response Process | PICERL framework (Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned) |
| 6 | Conclusion | Recap |

## Key Concepts

**Artifacts**  
Traces of attacker activity left on a system (processes, registry keys, logs, files, network connections). These are the raw material every forensic analysis starts from.

**Order of volatility**  
Data disappears at different rates. Capture sequence is critical: RAM → running processes → network state → disk. Dictates what must be collected first before evidence is lost forever.

**Chain of custody**  
Documented handling of evidence (who had it, when, how it was transferred). Without a clean chain, findings become untrustworthy and potentially inadmissible.

**Evidence preservation**  
Always work on forensic copies, never the original media. Hashing (MD5/SHA) is used at every handoff to prove integrity has been maintained.

**Timeline creation**  
Correlating artifacts from multiple sources into a single chronological narrative. This is the investigator’s primary analytical output and the foundation for understanding attacker behaviour.

**PICERL**  
The standard Incident Response lifecycle (SANS / NIST-aligned):  
Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned.

**Tool landscape**  
- **Eric Zimmerman’s tools** — high-quality Windows artifact parsers  
- **KAPE** — rapid triage collection + parsing (60+ targets, 90+ modules)  
- **Autopsy** — open-source disk image analysis platform  
- **Volatility** — memory forensics framework (Windows + Linux)  
- **Redline** — endpoint analysis / lightweight EDR-style collection  
- **Velociraptor** — fleet-scale hunting with VQL (now under Rapid7)

## Skills & Mapping

artifact identification · order of volatility · chain of custody · timeline building · PICERL lifecycle · KAPE / Volatility / Velociraptor

**Role mappings**  
- DFIR analyst / incident responder → artifact triage, timeline reconstruction, containment decisions  
- SOC Level 1 → IR process awareness and escalation criteria  
- Threat hunter → Velociraptor VQL for fleet-wide hunts  
- Forensic examiner → evidence handling, KAPE collection, Autopsy disk analysis

## References

- NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide: https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final  
- SANS PICERL model: https://www.sans.org/information-security/  
- KAPE documentation: https://ericzimmerman.github.io/KapeDocs/  
- Velociraptor documentation: https://docs.velociraptor.app/
