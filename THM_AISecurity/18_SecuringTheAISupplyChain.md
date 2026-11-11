# TryHackMe – Securing the AI Supply Chain

**Platform**: TryHackMe  
**Difficulty**: Medium  
**Category**: AI Security / Supply Chain  
**Date**: 10 Nov 2026  
**Time spent**: ~1 hour  
**Tags**: `#AI-Supply-Chain` `#SafeTensors` `#ModelScan` `#SBOM` `#Fickling` `#Defensive`

---

## Summary & Key Takeaways

This room is the defensive counterpart to the earlier attack-vector rooms. After the (fictional) TryTrainMe breach involving a malicious pickle, fake repository, and dependency confusion, you are tasked with building **SupplySecLab** — a layered set of controls that close every gap that allowed the incident to occur.

**Key Takeaways**
- Prefer **SafeTensors** (or `weights_only=True`) over pickle — it removes the code-execution surface entirely.
- Treat every new model as untrusted: **Quarantine → Verify (checksum + model card) → Scan → Inspect architecture**.
- Static scanners (Fickling + ModelScan) catch many, but not all, threats. Architecture-level inspection is still required.
- Dependencies must be version-pinned and audited (`pip-audit`); generate SBOMs (preferably CycloneDX).
- API-consumed models require behavioural baselines and version-controlled system prompts — silent updates are otherwise invisible.

---

## Core Concepts

| Layer                    | Primary Risk                              | Key Control(s)                                      |
|--------------------------|-------------------------------------------|-----------------------------------------------------|
| Serialisation            | Arbitrary code execution on load          | SafeTensors / `weights_only=True`                   |
| Provenance & Integrity   | Tampered or substituted model files       | SHA-256 checksums + model-card review + quarantine  |
| Static Analysis          | Malicious code inside model files         | Fickling + ModelScan                                |
| Architecture             | Hidden Lambda / custom layers             | Manual / scripted architecture inspection           |
| Dependencies             | Dependency confusion / known CVEs         | Version pinning + `pip-audit` + SBOM (CycloneDX)    |
| API Providers            | Silent model swaps / prompt tampering     | Behavioural baselines + version-controlled prompts  |

---

## Environment Setup

- Linux VM with pre-installed tools: `pickletools`, `fickling`, `modelscan`, `sha256sum`, `inspect_h5_model.py`, `pip-audit`, `syft`
- Additional AI Agents available for live behavioural analysis and API-provider assessment
- Model files and requirements located under the lab directories

---

## Step-by-Step Methodology

### 1. Safe Serialisation Formats
- Replace pickle with **SafeTensors** wherever possible.
- When pickle is unavoidable, load with `torch.load(..., weights_only=True)`.

### 2. Model Verification & Provenance
- First action on receipt of any model → **Quarantine**.
- Compare SHA-256 against expected values.
- Review the accompanying model card for provenance, intended use, and known limitations.

### 3. Behavioural Analysis
- Observe what object is actually returned on load (telemetry can reveal non-model objects such as `int`).

### 4. Scanning Models Before Use
- Run **Fickling** (Trail of Bits) for static analysis of pickle files.
- Run **ModelScan** — treat `os.system` (and similar) as **CRITICAL**.

### 5–6. Architecture-Level Threats & Inspection
- Inspect layer count and types.
- Use `inspect_h5_model.py` (or equivalent) to surface suspicious custom / Lambda layers (e.g. `manipulate_output`).

### 7. Dependency Auditing & SBOMs
- Enforce **version pinning** in `requirements.txt`.
- Scan with `pip-audit`.
- Generate SBOMs; prefer **CycloneDX** (security-focused, OWASP-maintained).

### 8. API Provider Assessment
- Establish a **behavioural baseline** so silent model updates become detectable.
- Treat system prompts as code: version-control and review them.
- Evaluate provider configurations against a supply-chain checklist.

---

## What Went Wrong (in the preceding incident)

- No policy on acceptable serialisation formats
- Models deployed without integrity checks
- No pre-deployment scanning
- Architecture never inspected for hidden logic
- Dependencies never audited
- External prompts / API models accepted without review or monitoring

---

## Remediation / SupplySecLab Controls

1. Mandate SafeTensors (or `weights_only=True`)
2. Enforce quarantine + checksum + model-card gate
3. Integrate Fickling + ModelScan into the CI/CD pipeline
4. Add architecture inspection for `.h5` / custom-layer models
5. Pin dependencies + run `pip-audit` + generate CycloneDX SBOMs
6. Require behavioural baselines and version-controlled system prompts for any API-consumed model

---

## References

- Room: https://tryhackme.com/room/securing-the-ai-supplychain
- Related: Supply Chain Attack Vectors, Payload, Checkpoint
- Tools: SafeTensors, Fickling, ModelScan, pip-audit, Syft / CycloneDX
