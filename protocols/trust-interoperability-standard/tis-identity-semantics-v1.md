---
title: "Identity Semantics v1"
registry_id: "TIS-TIS-IDENTITY-SEMANTICS-V1"
status: "draft"
category: "trust-interoperability-standard"
canonical_format: "markdown"
legacy_name_contains: "DeepTrust"
---
# Identity Semantics v1

> **Provenance note:** This document preserves historical naming from earlier drafts. References such as `Abracadabradoo`, `DeepTrust`, or `Dialogica` may indicate legacy project names, source-document context, or sibling protocol material rather than current public positioning.
*(Referenced by TIS, Dialogica, DeepTrust)*

## Purpose

This profile defines how identity is represented, referenced, and contextualized across trust-based systems. It enables support for both **cryptographically verifiable** and **symbolic or ritual** identity forms—allowing protocols to model *who* is involved in a trust exchange without prescribing a single identity model.

## Design Principles

- **Pluralism**: Identity can be verifiable, pseudonymous, symbolic, or anonymous.

- **Contextuality**: Identity is valid only *within the frame* of a TOA, thread, or claim.

- **Embodiment**: Gesture, ritual, or co-presence may serve as identification.

- **Non-coercion**: Systems must not require a single identity form unless explicitly scoped.

## Identity Schema Fields

## actor_id

A unique reference to the participant in the trust exchange.  
Examples:

actor_id: "did:key:z6Mkabc..."

actor_id: "persona:wind-walker"

actor_id: "ritual:circleA"

## identity_model

Describes how the identity is constructed and verified.

identity_model:

type: "verifiable" \# or 'pseudonymous', 'symbolic', 'anonymous'

verification: "signature"

backing: "DAO-issued credential"

## binding_method

Indicates how identity is linked to the TOA or message:

binding_method:

\- "signature on TOA payload"

\- "referenced in thread-link"

\- "verbal declaration"

\- "gesture in shared space"

## persona_label *(optional)*

Symbolic or role-based identity used in a given context:

persona_label: "sky-walker"

persona_scope: "within this moon cycle only"

## Identity Types

| **Type**     | **Description**                           |
|--------------|-------------------------------------------|
| verifiable   | DID, public key, or credential-backed     |
| pseudonymous | Stable handle; not necessarily verified   |
| symbolic     | Name or role chosen within a ritual/group |
| anonymous    | No persistent reference; fully ephemeral  |

## Verification Methods

- signature – e.g. DID, VC, or JWT

- gesture – e.g. physical act like hand clasp or salute

- ritual – e.g. circle chant, oath

- presence – verified by shared co-location or time

## Example Identity Block in a TOA

identity:

actor_id: "did:key:z6Mk..."

identity_model:

type: "pseudonymous"

verification: "none"

binding_method:

\- "included in thread turn"

persona_label: "first-speaker"

## Cross-System Mapping

| System        | Usage                                          |
|---------------|------------------------------------------------|
| **TIS**       | Actor ID + binding in trust object archetypes  |
| **Dialogica** | Role resolution in structured dialogue threads |
| **DeepTrust** | Anchor for audit trail or claim verification   |

## Future Directions

- Identity lifecycle tracking (e.g. persona expiration)

- Symbolic registries for social or cultural roles

- Automatic trust scoring or credibility anchoring

- Event-triggered identity transitions (e.g. “first-meeting.v1”)

---

_Source converted from `Identity Semantics v1.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
