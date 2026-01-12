# RFC-PBI-1.0  
## Presence-Bound Identity (PBI)  
### A Specification for Human-Origin Verification

**Status:** Final  
**Category:** Standards Track  
**Version:** 1.0  
**Audience:** Implementers, Protocol Designers, Auditors  
**Last Updated:** 2026-01-11  

---

## Abstract

This document specifies **Presence-Bound Identity (PBI)**, a verification primitive in which artifact truth is publicly verifiable, identity remains private, and ownership resolution requires embodied human presence on a local device. PBI eliminates impersonation, transferable credentials, and centralized identity by design. This specification defines the lifecycle, state model, compliance requirements, and prohibited behaviors for PBI-compliant systems.

---

## 1. Introduction

Digital identity systems have historically conflated **truth**, **identity**, and **presence**, resulting in impersonation, replay, surveillance, and fraud. These systems verify credentials rather than humans.

Presence-Bound Identity separates these concerns into orthogonal layers and treats **presence** as a first-class, non-transferable property. This RFC defines the **minimum and sufficient requirements** for implementing PBI without weakening its invariants.

---

## 2. Terminology

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **MAY**, and **OPTIONAL** are to be interpreted as described in RFC 2119.

- **Artifact**: A publicly shareable object (e.g., sigil-glyph) containing proof material.
- **Verifier**: A stateless surface that validates artifacts and optionally resolves presence locally.
- **Φ-Key (Phi-Key)**: A deterministic identity root resolved only via local presence.
- **Presence Proof**: A non-exportable, device-local proof of embodied human presence.
- **Ownership Resolution**: The momentary confirmation that the creator of an artifact is present on the observing device.

---

## 3. System Overview

A PBI system consists of **three independent processes**:

1. **Artifact Verification** — public and deterministic  
2. **Identity Protection** — private and non-derivable  
3. **Presence Resolution** — local and embodied  

No process implies or substitutes for another.

---

## 4. Artifact Model

### 4.1 Artifact Requirements

An artifact:

- MUST be verifiable by any observer without authentication.
- MUST contain sufficient proof material to validate authenticity.
- MUST NOT contain identity, biometric, or personal data.
- MAY be copied or shared freely without loss of verifiability.

---

### 4.2 Artifact Verification

Artifact verification:

- MUST be deterministic.
- MUST produce identical results for all observers.
- MUST NOT depend on:
  - accounts,
  - sessions,
  - IP addresses,
  - prior interactions,
  - device fingerprints.

---

## 5. Verifier Requirements

### 5.1 Statelessness

A verifier:

- MUST be stateless with respect to identity and ownership.
- MUST NOT store user profiles, sessions, or credentials.
- MAY cache non-identity proof material for performance.

---

### 5.2 Verification Flow (Normative)

A verifier MUST perform the following steps in order:

1. Parse artifact proof material.
2. Validate artifact proofs.
3. Display **Verified** state.
4. OPTIONALLY request local presence.
5. If presence resolves, display **Verified + Owned**.

No step may be skipped, reordered, or implied.

---

## 6. Presence Resolution

### 6.1 Locality

Presence resolution:

- MUST occur on the observing device.
- MUST use device-native, non-exportable mechanisms.
- MUST NOT be performed remotely or delegated.

---

### 6.2 Ephemerality

Presence proofs:

- MUST be ephemeral.
- MUST NOT be replayable.
- MUST expire immediately after resolution.

---

### 6.3 Ownership Scope

Ownership resolution:

- MUST apply only to the current device and moment.
- MUST NOT persist across reloads, devices, or sessions.

---

## 7. State Model

Only the following states are permitted.

---

### 7.1 Verified

- Artifact Truth: Resolved  
- Presence: Not resolved  
- Ownership: Not resolved  

---

### 7.2 Verified + Owned

- Artifact Truth: Resolved  
- Presence: Resolved locally  
- Ownership: Momentarily resolved  

---

### 7.3 Prohibited States

The following states MUST NOT exist:

- Logged in
- Authenticated user
- Persistent owner
- Remote ownership
- Delegated presence

---

## 8. Compliance Requirements

A system is **PBI-compliant if and only if** all of the following hold:

1. Public artifact verification without login  
2. No embedded or stored identity data  
3. Ownership resolves only via local presence  
4. Presence proofs are non-exportable  
5. Verifiers are stateless  
6. Ownership is non-transferable  
7. No accounts, sessions, or credentials exist  

Compliance is binary.

---

## 9. Security Considerations

PBI eliminates the following attack classes **by construction**:

- Impersonation
- Credential theft
- Replay attacks
- Session hijacking
- Deepfake escalation
- Database compromise

No mitigation strategies are required because the necessary primitives do not exist.

---

## 10. Privacy Considerations

PBI systems:

- Do not store biometric data.
- Do not transmit biometric data.
- Do not create identity graphs.
- Do not enable cross-artifact correlation.

Presence remains local, ephemeral, and private.

---

## 11. Interoperability

### 11.1 Allowed Extensions

Implementations MAY:

- Support additional artifact formats.
- Support additional proof systems.
- Support additional device presence methods.

---

### 11.2 Disallowed Extensions

Implementations MUST NOT:

- Introduce accounts.
- Introduce transferable credentials.
- Introduce centralized identity stores.
- Introduce persistent ownership.

---

## 12. Reference Implementation Alignment

The live PBI system demonstrates compliance through:

- URL-based public verification
- Deterministic artifact proofs
- Device-native presence resolution
- Absence of identity databases
- Distinct public vs presence-resolved states

This RFC codifies existing behavior; it does not invent new mechanisms.

---

## 13. IANA Considerations

This document requires no IANA actions.

---

## 14. Conclusion

Presence-Bound Identity defines a verification primitive in which:

- Truth is public  
- Identity is private  
- Ownership is embodied  
- Presence is required  
- Impersonation is impossible  

This RFC establishes the technical standard for PBI-compliant systems.

---

## Status of This Document

This specification is **final**, **normative**, and **complete**.  
Future versions may extend capabilities but **must not weaken presence**.

---
