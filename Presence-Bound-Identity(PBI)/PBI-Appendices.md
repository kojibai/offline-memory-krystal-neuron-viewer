# PBI-1.0 Appendices  
## Canonical Definitions, Invariants, and Compliance

**Version:** PBI-1.0  
**Status:** Normative  
**Audience:** Technical, Legal, Auditors, Implementers  
**Scope:** Binding for all PBI-compliant systems

> **Normative Notice**  
> These appendices are **binding**.  
> Any implementation, explanation, or claim of Presence-Bound Identity (PBI) **must conform** to the contents of this document.  
> Partial adherence constitutes non-compliance.

---

# Appendix A  
## Canonical Definition, Model, and Invariants of Presence-Bound Identity (PBI)

---

## A.1 Canonical Definition

**Presence-Bound Identity (PBI)** is a verification primitive in which:

- Artifacts are publicly verifiable without accounts or authorities  
- Identity is never embedded, transmitted, or stored  
- Ownership resolution is contingent on embodied human presence  
- Presence is proven locally through non-exportable, device-native proof  
- Impersonation is structurally impossible by design  

PBI does **not** authenticate accounts, keys, or sessions.  
PBI resolves **presence**.

---

## A.2 Scope and Non-Goals

### What PBI Is

- A primitive for human-origin verification  
- A system for separating truth, identity, and presence  
- A mechanism for proving authorship without transferability  
- A verifier model that functions without databases  
- A standard that treats presence as a first-class property  

### What PBI Is Not

- An account system  
- A wallet login  
- OAuth, SSO, or identity federation  
- A biometric database  
- An NFT ownership model  
- A reputation or scoring system  
- A platform-issued credential  
- A system dependent on trusted third parties  

Any system requiring user accounts, centralized identity stores, or transferable credentials **cannot qualify** as PBI-compliant.

---

## A.3 Core Entities (Live System Terms)

### Artifact

A sigil-glyph or equivalent artifact containing:

- Canonical proof payload  
- Deterministic identifiers  
- Verifiable sealing data  

Artifacts may be copied freely without loss of verifiability.

---

### Verifier

A stateless verification surface (web or native) that:

- Performs proof validation  
- Resolves artifact state  
- Optionally queries local presence  

The verifier **must not** store users, sessions, or identities.

---

### Φ-Key (Phi-Key)

A deterministic identity root bound to a human and resolved only through local presence.

Φ-Keys:

- Are not passwords  
- Are not transferable secrets  
- Cannot be reconstructed from artifacts  
- Cannot be resolved remotely  

---

### Presence Proof

A local, non-exportable proof produced when a human is physically present and satisfies device-native authentication.

Presence proofs:

- Never leave the device  
- Cannot be replayed  
- Cannot be forwarded  
- Cannot be simulated by servers  

---

## A.4 Three-Layer Verification Model

PBI verification always resolves into **three independent layers**.

No layer may imply another.

---

### Layer 1: Artifact Truth (Public)

**Invariant A1**  
An artifact must be verifiable by any observer without authentication.

Confirms:

- Existence  
- Authenticity  
- Device-local presence enforcement at sealing  
- Proof validity  

Artifact Truth is independent of ownership.

---

### Layer 2: Identity Truth (Private)

**Invariant A2**  
Identity must never be derivable from the artifact.

Ensures:

- No personal identifiers embedded  
- No recoverable biometric data  
- No server-side identity resolution  
- No cross-view correlation  

---

### Layer 3: Presence Truth (Embodied)

**Invariant A3**  
Ownership resolution requires live, local human presence.

Resolves only if:

- The human is physically present  
- The device satisfies its local authentication guarantee  
- The Φ-Key resolves on that device  

If presence is absent, ownership **must not** resolve.

---

## A.5 State Model (Normative)

A PBI verifier may display **only** the following states:

### State 1: Verified (Public)

- Artifact Truth: ✔  
- Identity Truth: Protected  
- Presence Truth: ✖  

Ownership does not resolve.

---

### State 2: Verified + Owned (Presence-Resolved)

- Artifact Truth: ✔  
- Identity Truth: Protected  
- Presence Truth: ✔  

Ownership resolves **only on that device and moment**.

---

### Disallowed States

The following are **explicitly invalid**:

- Logged in  
- Owner authenticated remotely  
- Identity verified without presence  
- Ownership transferred  
- Persistent session ownership  

---

## A.6 Threat Model (Eliminated by Construction)

The following attack classes are structurally impossible:

- Impersonation via copied artifacts  
- Identity theft via shared links  
- Replay attacks (screenshots, recordings)  
- Session hijacking  
- Credential stuffing  
- Database compromise  
- Deepfake identity escalation  
- Remote ownership claims  

This is due to **absence of attack surface**, not mitigation.

---

## A.7 Invariants (Must Always Hold)

1. Presence cannot be forwarded  
2. Ownership cannot be transferred  
3. Identity cannot be extracted  
4. Verification requires no permission  
5. Verifiers remain stateless  
6. Proofs remain publicly inspectable  
7. Presence remains local and embodied  

Violation of any invariant **disqualifies** PBI classification.

---

## A.8 Reference Implementation Alignment

The live PBI system demonstrates all invariants through:

- URL-based public verification  
- Artifact-level proof resolution  
- Device-native biometric presence checks  
- Absence of user accounts or databases  
- Distinct public vs presence-resolved states  

Compliance is by **construction**, not policy.

---

## A.9 Canonical Closing Statement

Presence-Bound Identity establishes a verification model in which:

- Truth is public  
- Identity is private  
- Ownership is embodied  
- Impersonation is impossible  

This appendix defines the primitive.  
All subsequent documents **must conform** to it.

---

# Appendix B  
## Operational Guarantees & Compliance Criteria

---

## B.1 Operational Guarantees

### B.1.1 Stateless Verification

- Verifiers must not persist identity, ownership, or session data  
- Results derive only from:
  - the artifact  
  - the proof payload  
  - optional local presence  

Any server-side identity memory violates PBI.

---

### B.1.2 Deterministic Artifact Verification

- Identical results for all observers  
- No observer-specific state  
- No dependency on:
  - accounts  
  - prior interactions  
  - IP address  
  - device fingerprinting  

---

### B.1.3 Local Presence Resolution

- Presence resolves only on the observing device  
- Presence proofs must be:
  - non-exportable  
  - non-replayable  
  - immediately expired  

Remote presence resolution is prohibited.

---

### B.1.4 Ownership Non-Persistence

- Ownership does not persist beyond presence  
- Reloads or new devices require fresh presence  
- “Remembered ownership” is prohibited  

---

## B.2 Compliance Requirements

A system is **PBI-compliant if and only if** all hold:

1. Public artifact verification without login  
2. No embedded or stored identity data  
3. Ownership resolves only through live presence  
4. Presence proofs are device-local and ephemeral  
5. No transferable credentials exist  
6. Verifiers are stateless  
7. Ownership cannot be delegated or proxied  

Compliance is binary.

---

## B.3 Explicit Non-Compliance Examples

- Wallet-based logins  
- Account + biometric hybrids  
- OAuth with passkeys  
- NFT ownership models  
- Centralized “verified creator” systems  
- Reputation or trust-score systems  
- Session-based authentication  

---

## B.4 Canonical Compliance Statement

> Presence-Bound Identity compliance is binary.  
> Partial implementation is non-compliance.

---

# Appendix C  
## Threat Model & Security Properties

---

## C.1 Threat Classes Eliminated

- Identity impersonation  
- Credential theft  
- Session hijacking  
- Replay attacks  
- Deepfake escalation  
- Artifact forgery  
- Ownership forwarding  
- Database compromise  

---

## C.2 Why These Attacks Fail

| Attack | Reason |
|------|-------|
| Impersonation | Presence cannot be copied |
| Replay | Proofs are local & ephemeral |
| Phishing | No credentials exist |
| Deepfakes | Presence is embodied |
| DB breach | No identity database |
| Key theft | No transferable keys |

---

## C.3 Adversarial Assumptions

Adversaries may:

- Copy artifacts  
- Know proof formats  
- Control servers  
- Observe networks  
- Attempt social engineering  

PBI remains secure.

---

## C.4 Security Invariant

> If presence is not physically satisfied, ownership must not resolve.

---

# Appendix D  
## User-Visible State Semantics

---

## D.1 Allowed States

### Verified
- Artifact Truth resolved  
- Presence not resolved  
- Ownership unknown  

### Verified + Owned
- Artifact Truth resolved  
- Presence resolved locally  
- Ownership momentary  

---

## D.2 Prohibited Language

- Logged in  
- Authenticated user  
- Owner account  
- Session active  
- Identity verified remotely  

---

## D.3 UX Invariant

UI must not imply ownership persistence.

---

# Appendix E  
## Privacy Properties & Data Minimalism

---

## E.1 Zero Identity Disclosure

PBI systems must not:

- Store biometric data  
- Transmit biometric data  
- Correlate identity across artifacts  
- Infer identity from behavior  

---

## E.2 Data Minimization Principle

Only permitted data:

- Artifact data  
- Public proof data  
- Ephemeral local presence confirmation  

All else is prohibited.

---

## E.3 Regulatory Positioning

PBI systems:

- Do not process biometric data centrally  
- Do not store personal data  
- Do not require consent banners  
- Do not create identity profiles  

---

# Appendix F  
## Interoperability & Future Extensions

---

## F.1 Allowed Extensions

- New artifact formats  
- New proof systems  
- Additional device presence methods  

---

## F.2 Disallowed Extensions

- Accounts  
- Persistent ownership  
- Delegated presence  
- Centralized identity stores  

---

## F.3 Forward Compatibility Rule

> Extensions may add capabilities but must never weaken presence.

---

# Appendix G  
## Canonical Summary

Presence-Bound Identity establishes a verification primitive where:

- Truth is public  
- Identity is private  
- Ownership is embodied  
- Presence is required  
- Impersonation is impossible  
- Verification is stateless  
- Trust is structural, not social  

These appendices define **what PBI is**, **what it is not**, and **what it must always remain**.

---
