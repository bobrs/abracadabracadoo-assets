---
title: "Dialog Turn v1"
registry_id: "TIS-TIS-DIALOG-TURN-V1"
status: "draft"
category: "trust-interoperability-standard"
canonical_format: "markdown"
---
# Dialog Turn v1

*(Part of Dialogica Threading Model — interoperable with TIS)*

## Purpose

This specification defines the structure of a single **turn** in a Dialogica thread. A turn is the smallest unit of expression in structured dialogue and can carry embedded **trust semantics**, **identity assertions**, or **consent references**.

## Key Design Principles

- **Atomic**: Represents one unit of speech, proposal, or assertion

- **Verifiable**: Can be signed, anchored, or hashed

- **Contextual**: Interpreted within a thread’s scope and history

- **Composable**: Interoperable with TIS TOAs, identity models, and reputation records

## Data Structure

dialog_turn:

turn_id: "turn-042"

thread_id: "thread-tribunal-7"

sequence: 42

timestamp: "2025-05-03T13:45:00Z"

speaker: "did:key:z6Mk..."

role: "initiator"

content: \|

I move to close the witness phase of the session.

trust_marker:

archetype_id: "dialog-anchor.v1"

consent_mode:

type: "explicit"

mechanisms: \["message-signature"\]

identity:

actor_id: "did:key:z6Mk..."

identity_model:

type: "verifiable"

verification: "signature"

temporal_profile:

duration: "sessional"

confirmation_of: "turn-040"

annotations:

sentiment: "assertive"

intent: "propose-closure"

scope: "dialog-phase"

## Core Fields

| **Field**       | **Description**                                      |
|-----------------|------------------------------------------------------|
| turn_id         | Unique reference within thread                       |
| thread_id       | Foreign key to thread container                      |
| sequence        | Order in which this turn appears                     |
| timestamp       | When the turn was made (or signed)                   |
| speaker         | DID or identity string of the turn author            |
| role            | Dialogical role (e.g. initiator, observer, arbiter)  |
| content         | Natural language or symbolic utterance               |
| trust_marker    | Embedded TOA-based trust signature or anchoring      |
| confirmation_of | Optional reference to a prior turn this one confirms |
| annotations     | AI/agent metadata (optional)                         |

## Trust Marker Compatibility

- Uses TIS-compatible fields (e.g. archetype_id, consent_mode, identity)

- Enables per-turn traceability, consent tracking, or reputation events

- confirmation_of links this turn to a prior one that is being explicitly acknowledged or finalized

## Example Use Cases

- A tribunal member asserting a binding vote

- An agent verifying their identity in a first message

- A speaker embedding a TOA consent signal mid-thread

- A DAO contributor initiating a phase change or escalation

- A participant acknowledging a previous offer or assertion using confirmation_of

## Future Extensions

- Turn hash linking (Merkle-style thread proofs)

- Multi-modal content blocks (e.g. gestures, audio, symbolic state)

- Conditional turns (if, unless, when semantics)

- Delegation chains and witness validation

---

_Source converted from `Dialog Turn v1.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
