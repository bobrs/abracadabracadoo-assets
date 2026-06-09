---
title: "Consent Semantics v1"
registry_id: "TIS-TIS-CONSENT-SEMANTICS-V1"
status: "draft"
category: "trust-interoperability-standard"
canonical_format: "markdown"
legacy_name_contains: "DeepTrust"
---
# Consent Semantics v1

> **Provenance note:** This document preserves historical naming from earlier drafts. References such as `Abracadabradoo`, `DeepTrust`, or `Dialogica` may indicate legacy project names, source-document context, or sibling protocol material rather than current public positioning.
*(Referenced by TIS, Dialogica, DeepTrust)*

## Purpose

This semantic profile formalizes the modeling of **consent** in trust-based systems. It recognizes consent as a multidimensional concept—*not merely a legal construct, but a semantic and social signal*—that transforms interactions into trusted relationships. It is applicable across TOAs, dialogic protocols, and agent interactions.

## Design Principles

- **Multimodal**: Consent can be verbal, cryptographic, symbolic, or embodied.

- **Negotiable**: Consent may be offered, requested, revoked, or contextualized.

- **Expressive**: Consent reflects power, intent, and trust boundaries.

- **Context-aware**: Meaning changes across cultural, legal, and interactional frames.

## Consent Schema Fields

## consent_mode

Indicates the form of consent exchange within a TOA or protocol.

consent_mode:

type: "explicit"

mechanisms: \["QR scan", "verbal acknowledgment", "ritual gesture"\]

confirmation_required: true

confirmation_mechanism: \["verbal reply", "digital signature"\]

## Common Consent Types

| **Type**  | **Description**                                 |
|-----------|-------------------------------------------------|
| explicit  | Direct affirmation via voice, click, signature  |
| symbolic  | Action with shared social meaning (e.g. salute) |
| embodied  | Co-presence, gaze, gesture, synchronized action |
| delegated | Granted by trusted third party or credential    |
| implied   | Inferred through participation or context       |

## revocability

Specifies whether and how consent can be withdrawn.

revocability:

method: \["manual", "time expiry"\]

recovery_possible: false

## Consent Confirmation

Some consent interactions require acknowledgment or acceptance to be semantically valid. This confirmation may occur:

- As a verbal or signed response

- Through gesture or symbolic act

- As a follow-up turn in a dialogue (e.g. confirmation_of: turn-7)

TOAs may specify:

- confirmation_required: true

- confirmation_mechanism: \[...\]

In formal systems, confirmation may also be modeled as a distinct TOA (e.g. consent-ack.v1) or as a signed audit entry.

## Consent Spectrum

Consent exists along multiple intersecting axes:

- **Directionality**: one-way, mutual, multilateral

- **Formality**: informal, ritualized, institutional

- **Temporal Scope**: ephemeral, sessional, persistent

- **Traceability**: unrecorded, logged, signed

## Example Models in TOAs

## explicit – TotemSync

consent_mode:

type: "explicit"

mechanisms: \["QR scan"\]

confirmation_required: true

confirmation_mechanism: \["match TOTP", "verbal reply"\]

## symbolic – PhrasePair

consent_mode:

type: "symbolic"

mechanisms: \["spoken phrase"\]

## embodied – SpiritLink

consent_mode:

type: "embodied"

mechanisms: \["shared gaze", "ritual chant"\]

## delegated – DelegateBond

consent_mode:

type: "delegated"

mechanisms: \["signed VC"\]

## Cross-System Mapping

| System        | Usage                                          |
|---------------|------------------------------------------------|
| **TIS**       | Declares consent type in TOA trust exchange    |
| **Dialogica** | Consent embedded in dialogue turn context      |
| **DeepTrust** | Consent tied to identity audit or access token |

## Advanced Topics

- Consent decay or renewal cycles

- Non-consent (explicit refusal)

- Conditional or scoped consent ("for this purpose only")

- Meta-consent (consenting to being asked, or to context adaptation)

## Future Directions

- Integration with ODRL and Data Privacy Vocabularies

- Formal modeling of refusal and objection

- Ritualized revocation events (e.g. “unbinding ceremonies”)

- Consent provenance and dispute mediation

---

_Source converted from `Consent Semantics v1.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
