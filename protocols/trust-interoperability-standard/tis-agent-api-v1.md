---
title: "TIS Agent API v1"
registry_id: "TIS-TIS-AGENT-API-V1"
status: "draft"
category: "trust-interoperability-standard"
canonical_format: "markdown"
legacy_name_contains: "DeepTrust"
---
# TIS Agent API v1

> **Provenance note:** This document preserves historical naming from earlier drafts. References such as `Abracadabradoo`, `DeepTrust`, or `Dialogica` may indicate legacy project names, source-document context, or sibling protocol material rather than current public positioning.

## Purpose

This lightweight interface enables agents (human or autonomous) to **propose**, **negotiate**, and **record** trust events using TOAs. It complements the TIS core schema by standardizing runtime interactions for trust exchange.

## Design Goals

- **Minimal**: Portable to constrained devices or low-bandwidth environments

- **Semantic-first**: Emphasizes meaning over mechanics

- **Composable**: Integrates with identity, consent, and reputation layers

- **Interoperable**: Aligns with DIDComm, HTTP, and message-based protocols

## Core Concepts

- **Trust Offer**: A structured invitation to enter a TOA

- **Trust Confirmation**: A mutual or unilateral signal of agreement

- **Trust Record**: A signed, timestamped, or referenced outcome

- **Consent Interpretation**: Agents must interpret declared consent_mode and decide whether to proceed

## API Methods (Conceptual)

## POST /trust-offer

Proposes a TOA to one or more participants.

{

"to": \["did:key:z6Mk..."\],

"archetype_id": "totem-sync.v1",

"payload": {

"identity": { ... },

"consent_mode": {

"type": "explicit",

"mechanisms": \["QR scan"\]

},

"temporal_profile": {

"duration": "sessional"

}

},

"expires": "2025-06-01T00:00:00Z"

}

## POST /trust-confirmation

Confirms acceptance and includes any reciprocal trust data.

{

"offer_id": "abc123",

"accepted": true,

"signed_by": "did:key:z6Mkt...",

"confirmation_note": "Matched TOTP successfully"

}

## GET /trust-log?actor=did:key:z6Mk...

Returns traceable records of prior TOA exchanges (if consented/logged).

## Agent Roles

| **Role**  | **Description**                          |
|-----------|------------------------------------------|
| Initiator | Proposes a trust offer                   |
| Responder | Accepts, modifies, or rejects a proposal |
| Recorder  | Logs or anchors the trust exchange       |
| Observer  | May view the event with permission       |

## Sample Flow: Synchronous TOA Exchange

1.  Agent A posts a trust-offer for totem-sync.v1

2.  Agent B receives and evaluates the offer

3.  Agent B scans a shared TOTP seed (verbal/QR/NFC)

4.  Agent B posts a trust-confirmation

5.  Both agents log the event if traceability is enabled

## Integration Targets

- **Dialogica**: Turn-based trust triggers and anchoring

- **DeepTrust**: VC issuance or challenge validation post-consent

- **Wallets & Agents**: Lightweight API clients for trust exchange

## Future Directions

- WebSocket/stream support for ephemeral TOAs

- Negotiation primitives (counter-offer, multi-party confirmation)

- Secure DIDComm transport profile

- Event source signatures and replay resistance

---

_Source converted from `TIS Agent API v1.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
