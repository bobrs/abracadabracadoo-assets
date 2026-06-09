---
title: "Dialogica Integration Profile (TIS v1 Extension)"
registry_id: "TIS-TIS-DIALOGICA-INTEGRATION-PROFILE"
status: "draft"
category: "trust-interoperability-standard"
canonical_format: "markdown"
---
# Dialogica Integration Profile (TIS v1 Extension)

## Purpose

This profile describes how TIS-based trust semantics can be integrated into **Dialogica** threads—enabling structured, auditable, and semantically rich trust interactions within conversations. It supports AI mediation, civic dialogue, negotiation, and human-agent alignment.

## Design Goals

- **Turn-aware**: Trust can accumulate or shift across dialogue turns

- **Contextual**: Trust is tied to thread position, roles, and references

- **Semantic**: Allows agents to reason about identity, consent, and alignment

- **Interoperable**: Maps directly onto TIS trust archetypes and identity models

## Key Structures

## dialog_turn

A unit of exchange between participants in a Dialogica thread.

dialog_turn:

id: "turn-17"

speaker: "did:key:z6Mk..."

content: "I propose we ratify this path."

anchor: true

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

## thread_scope

A wrapper that defines trust context across a structured thread.

thread_scope:

thread_id: "tribunal-42"

participants:

\- did:key:z6Mk...

\- did:key:z9Tr...

lifecycle: "deliberation"

trust_accumulation: true

traceability: high

## anchor_event

An in-thread declaration of identity, intention, or consensus.

anchor_event:

type: "intent-declaration"

referenced_by: \["turn-3", "turn-7"\]

signed_by: "did:key:z9Tr..."

trust_payload:

archetype_id: "dialog-anchor.v1"

temporal_profile:

duration: "sessional"

## Use Cases

- AI-mediated dialogue with trust checkpoints

- Human-agent or tribunal trust anchoring

- Public or pseudonymous identity assertion within structured discourse

- Retrospective auditing of intent and alignment over time

## Mappable TOAs

| **Archetype ID** | **Role in Thread**                              |
|------------------|-------------------------------------------------|
| dialog-anchor.v1 | Identity or intent declaration (e.g. at turn 1) |
| thread-link.v1   | Trust formation across consistent behavior      |
| delegate-bond.v1 | Role-based authority grant or endorsement       |
| spirit-link.v1   | Symbolic pre-thread initiation                  |

## Future Directions

- GPT-style agent summaries of trust patterns in threads

- Visualization of trust_flow across dialogue states

- Declarative thread-certificates for outcomes

- Reputation scoring derived from multi-turn context

---

_Source converted from `Dialogica Integration Profile.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
