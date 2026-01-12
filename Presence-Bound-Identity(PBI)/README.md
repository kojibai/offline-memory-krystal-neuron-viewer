# Presence-Bound Identity (PBI)
## PBI-1.0 — Canonical Release Pack

**Status:** Final  
**Version:** 1.0  
**Scope:** Verification, Identity, Presence  
**Audience:** Public, Engineers, Auditors, Courts, Researchers

---

## What this repository is

This repository contains the **canonical definition, specification, legal framing, and public explanation** of **Presence-Bound Identity (PBI)**.

PBI is a **new verification primitive** that establishes a clean separation between:

- **Truth** — whether an artifact is real and unaltered  
- **Identity** — who created it (kept private)  
- **Presence** — whether that creator is physically present *now*

This is not an application, SDK, or library.  
This is the **foundational trust layer** that such systems can be built on.

---

## What Presence-Bound Identity (PBI) is

Presence-Bound Identity is a verification primitive in which:

- Artifacts are **publicly verifiable** without accounts or permission  
- Identity is **never embedded, stored, or transmitted**  
- Ownership (presence-resolved authorship) can **only** resolve through **embodied human presence** on a local device  
- Impersonation is eliminated **by construction**, not detection  

PBI does **not** authenticate accounts, sessions, or credentials.  
PBI resolves **presence**.

---

## What problem this solves

Most systems today verify **credentials** (accounts, keys, badges).

That model fails when:
- credentials are copied,
- accounts are compromised,
- media can be perfectly faked,
- AI can impersonate anyone.

PBI replaces credential-based trust with **presence-based verification**.

You cannot copy presence.  
You cannot forward presence.  
You cannot replay presence.

---

## Repository structure (how to read this)

This release pack is intentionally layered.  
Each file has a distinct role and **must be read in order**.

### 1. `PBI-Release.md` — The Declaration
The public statement of the primitive.

- Defines what PBI is
- States the core insight
- Explains the three-layer model
- Establishes the historical claim

This is the **entry point**.

---

### 2. `PBI-Appendices.md` — Canonical Definitions & Invariants
The **normative core** of PBI.

- Formal definition
- Invariants that must always hold
- Compliance requirements
- Threat model
- Prohibited behaviors and UI states

Any system claiming PBI compliance **must conform** to this file.

---

### 3. `RFC-PBI-1.0.md` — Technical Specification
The implementation-grade standard.

- Written in RFC style
- Uses normative language (MUST, MUST NOT, etc.)
- Defines lifecycle, flows, and state model
- Enables independent implementations without semantic drift

This is the file engineers build against.

---

### 4. `PBI-Legal.md` — Legal & Evidentiary Framing
Court-safe interpretation of PBI.

- Clarifies what PBI asserts and does not assert
- Explains evidentiary value
- Distinguishes PBI from biometric systems, accounts, and credentials
- Establishes non-equivalence boundaries

This file exists so PBI can be reasoned about **without misclassification**.

---

### 5. `PBI-Explainer.md` — Public Explanation
Plain-language explanation for non-technical readers.

- No jargon
- No hype
- No dilution

This file explains *what PBI means* without redefining it.

---

## Compliance and non-equivalence

PBI compliance is **binary**.

A system is **not** PBI-compliant if it includes:
- accounts,
- logins,
- transferable keys,
- persistent sessions,
- centralized identity stores,
- server-side ownership resolution.

Claiming equivalence without meeting the invariants defined in  
`PBI-Appendices.md` is materially misleading.

---

## What this repository is not

This repository is **not**:
- a product,
- a platform,
- a wallet,
- a biometric database,
- an identity provider,
- a reputation system.

It is the **definition of a primitive**.

---

## Versioning & stability

This repository defines **PBI-1.0**.

Future versions may:
- add new artifact formats,
- add new proof systems,
- support additional device presence mechanisms.

Future versions **must not**:
- weaken presence,
- introduce accounts,
- introduce transferable ownership,
- introduce centralized identity.

---

## Citation & reference

When referencing this work, cite:

> *Presence-Bound Identity (PBI), Version 1.0 — Canonical Release Pack*

For technical claims, reference:
- `PBI-Appendices.md`
- `RFC-PBI-1.0.md`

For legal interpretation, reference:
- `PBI-Legal.md`

---

## Final note

Presence-Bound Identity does not try to answer *who someone is*.

It answers a simpler and more reliable question:

> **Is the human who created this actually here — right now?**

This repository defines the system that makes that question provable.

---
