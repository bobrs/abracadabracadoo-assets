---
title: "Reputation Semantics v1"
registry_id: "TIS-TIS-REPUTATION-SEMANTICS-V1"
status: "draft"
category: "trust-interoperability-standard"
canonical_format: "markdown"
legacy_name_contains: "DeepTrust"
---
# Reputation Semantics v1

> **Provenance note:** This document preserves historical naming from earlier drafts. References such as `Abracadabradoo`, `DeepTrust`, or `Dialogica` may indicate legacy project names, source-document context, or sibling protocol material rather than current public positioning.
*(Extension of TIS, Dialogica, and DeepTrust)*

## Purpose

This profile outlines how **reputation** can be modeled, contextualized, and exchanged as a structured semantic layer atop trust interactions. It bridges subjective signals, cryptographic credentials, and social interpretation—enabling interoperable representations of credibility, consistency, and alignment.

## Design Principles

- **Subjective by default**: Reputation is context-dependent and shaped by evaluators.

- **Derived, not declared**: Reputation emerges from historical trust activity, not fiat claims.

- **Interoperable**: Compatible with VCs, logs, graphs, and narrative threads.

- **Pluralistic**: Allows for multi-perspective or agent-specific scoring and annotation.

## Core Fields

## reputation_record

A structured reference to trust-related activity that may influence perception.

reputation_record:

source: "dialogica:thread-347"

summary: "Agent demonstrated consistency and empathy"

score_hint: 0.85

endorsed_by: "did:org:community-coop"

timestamp: "2025-04-12T09:22:00Z"

## credibility_assertion

An explicit claim about another actor’s reliability or value.

credibility_assertion:

subject: "did:key:z6Mk..."

asserted_by: "did:key:z9Tr..."

claim: "responsive + transparent in conflict resolution"

signature: "0x83b0..."

## Reputation Vocabularies

- **Quantitative**: trust score, signal weight, rating (e.g. 4.8/5)

- **Qualitative**: endorsements, pattern recognition, narrative trace

- **Symbolic**: badges, roles, emoji, ceremonial titles

## Event Sources

Reputation can derive from:

- TOA completions (especially traceable or anchored)

- Dialogica threads with consistency scoring

- Signed attestations or social contracts

- Community rituals or voting logs

## Storage and Exchange Formats

- Embedded within TOA extensions or identity objects

- Published as Verifiable Credentials (VCs)

- Referenced in semantic graphs (via reputation_record URIs)

- Displayed in agent profiles or cooperative directories

## Example

identity:

actor_id: "did:key:z6Mk..."

reputation:

\- source: "dialogica:tribunal-log-23"

claim: "acted with non-dual empathy under tension"

endorsed_by: "peer-ring-A"

score_hint: 0.91

## System Roles

| **Role**     | **Description**                                   |
|--------------|---------------------------------------------------|
| **Emitter**  | Records reputation data or assertions             |
| **Subject**  | Receives or accrues reputation                    |
| **Context**  | Delimits the frame (e.g. dispute, mission, DAO)   |
| **Observer** | Agent who interprets reputation to make decisions |

## Trust-Reputation Interplay

- Trust events *generate* reputation signals

- Reputation may *bias* future trust formation

- Agents may annotate, boost, reject, or fork reputation inputs

## Future Directions

- Composable reputation modules in agent-based systems

- Narrative-based credibility networks

- ZK-privacy-preserving reputation proofs

- Multi-agent reputation fusion and bias modeling

---

_Source converted from `Reputation Semantics v1.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
