---
title: "Dialog Thread v1"
registry_id: "TIS-TIS-DIALOG-THREAD-V1"
status: "draft"
category: "trust-interoperability-standard"
canonical_format: "markdown"
---
# Dialog Thread v1

*(Part of Dialogica Threading Model — interoperable with TIS and identity semantics)*

## Purpose

This specification defines the structure of a **dialogue thread** in the Dialogica framework. Threads group one or more dialog turns into a meaningful, auditable, and optionally trust-bearing conversational unit. They can be anchored, signed, and analyzed across time and context.

## Design Principles

- **Container-first**: Threads provide structural and contextual framing

- **Multi-actor**: Threads may include human and/or autonomous participants

- **Semantic**: Threads include metadata for lifecycle, consent, and outcome

- **Composable**: Compatible with TOAs, reputation records, and audit tools

## Data Structure

dialog_thread:

thread_id: "tribunal-7"

created_at: "2025-05-01T09:00:00Z"

created_by: "did:key:z6Mk..."

participants:

\- did:key:z6Mk...

\- did:key:z7Lp...

\- did:key:z9Tr...

purpose: "resolve identity challenge for multisig onboarding"

lifecycle: "deliberation"

status: "active"

trust_events:

\- turn_id: "turn-001"

archetype_id: "dialog-anchor.v1"

\- turn_id: "turn-009"

archetype_id: "delegate-bond.v1"

\- turn_id: "turn-015"

archetype_id: "thread-link.v1"

traceability: "high"

integrity_hash: "sha256:9a4f..."

outcome: null

## Core Fields

| **Field**      | **Description**                                      |
|----------------|------------------------------------------------------|
| thread_id      | Globally unique thread identifier                    |
| created_at     | Timestamp of thread creation                         |
| created_by     | Initiator or originator of thread                    |
| participants   | List of DIDs or actors involved                      |
| purpose        | Human-readable thread intent                         |
| lifecycle      | Phase (e.g. initiation, deliberation, resolution)    |
| status         | Current thread state (e.g. active, closed, archived) |
| trust_events   | Indexed trust actions or anchors (via TOAs)          |
| traceability   | Degree of logging and verification support           |
| integrity_hash | Cryptographic summary of current thread state        |
| outcome        | Optional result or final declaration                 |

## Trust Event Anchoring

Trust markers (archetype_ids) in the thread reference specific turns. These may:

- Establish or revoke identity

- Declare consent

- Document endorsement, challenge, or resolution

## Lifecycle Examples

| Lifecycle    | Description                        |
|--------------|------------------------------------|
| initiation   | First contact or invitation        |
| deliberation | Multi-turn discussion phase        |
| resolution   | Decision-making, voting, consensus |
| ratified     | Finalized and anchored outcome     |

## Integration with TIS

- TOAs may be instantiated inline or referenced from turns

- thread-link.v1 and dialog-anchor.v1 provide natural bridges

- Supports identity, consent_mode, and persona_label at thread or turn scope

## Future Extensions

- DAO governance alignment (vote-cast.v1, proposal-passed.v1)

- Narrativized or symbolic threads (story-threads, ritual flows)

- Compression of thread snapshots via hash-linked rolls

- Agent summarization and trust synthesis reports

---

_Source converted from `Dialog Thread v1.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
