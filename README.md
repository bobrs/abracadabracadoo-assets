# Abracadabracadoo Assets

Public protocol documents, standard drafts, diagrams, media references, and reusable materials for the Abracadabracadoo consent-native trust stack.

This repository is the public shelf for the ecosystem: Abracadabracadoo, HumanKey, FractalIdentity, Abracadoo.app, and related consent-native communication patterns.

The working beta implementation lives at:

<https://github.com/bobrs/abracadoo-code>

## What this repo is for

- Canonical Markdown protocol and standard documents
- HumanKey and Trust Interoperability Standard drafts
- Generated PDF/DOCX exports, when needed
- Brand and site assets
- Diagrams, screenshots, and implementation reference materials
- Roadmap documentation for future layers such as FractalIdentity

## What this repo is not

This is not the application code repository. Use `abracadoo-code` for the functional beta implementation.

This repository is also not a standards body, legal filing system, or compliance authority. It is a public artifact shelf: readable, forkable, inspectable, and designed to support implementation work.

## Current implementation status

| Layer | Status | Notes |
|---|---|---|
| HumanKey | Live in beta | Relationship-sized authentication and reciprocal key relationships. |
| Abracadabracadoo | Live in beta | Consent-native communication and proof patterns. |
| FractalIdentity | Roadmap | Context-sized selfhood, plural channels, roles, aliases, and boundaries for future versions of the app. |
| Trust Interoperability Standard | Draft / publishing shelf | Semantic interoperability layer for trust offers, consent, identity, reputation, dialogue, and agent APIs. |
| Loop Training | Conceptual / training sequence | Six-part path from loop recognition to field identity, substrate awareness, and consent-coded training tools. |


## Public safety / security note

These materials include experimental cryptographic, authentication, consent, and trust-protocol work. Do not rely on them for production security-critical use without independent review and audit. See [`SECURITY.md`](SECURITY.md).

## Coherence notes

- Current ecosystem name: **Abracadabracadoo**. Historical drafts may preserve **Abracadabradoo** for provenance.
- `Abracadoo.app` is the free reference implementation, not the protocol itself.
- Two historical Addendum V documents are preserved as `05a` and `05b` pending any later registry migration.
- See [`docs/stack-map.md`](docs/stack-map.md) and [`docs/canon-stewardship-notes.md`](docs/canon-stewardship-notes.md).

## Repository map

```text
protocols/
  core/                 Core protocol specifications
  addenda/              Numbered protocol addenda and governance extensions
  extensions/           Practical extensions and optional layers
  whitepapers/          Public explainers and narrative documents
  legal/                Patent / legal reference drafts
  fractal-identity/     FractalIdentity draft materials
  human-key/            HumanKey draft and legacy reference materials
  trust-interoperability-standard/ Trust Interoperability Standard materials
  loop-training/       Loop reflexivity and field-awareness training materials

human-key/              HumanKey overview and media references
assets/
  brand/                Marks, logos, and reusable brand elements
  app-preview/          Abracadoo.app preview assets
  site/                 Assets reused from abracadabracadoo.com
media/                  Large media reference notes and future video placement
originals/              Original source files retained for provenance
exports/                Generated PDFs or other publishable exports
metadata/               Machine-readable indices
docs/                   Stack map and canon stewardship notes
```

## Canonical format

Markdown is the canonical public format for protocol documents in this repository.

Source `.docx` files are retained in `originals/docx/` for provenance. Generated PDFs may live in `exports/pdf/` when useful for sharing.

## Naming convention

Protocol Markdown files use lowercase, hyphenated, stable names:

```text
addendum-01-selective-semantic-recordkeeping.md
addendum-02-nested-loops-and-group-quorums.md
```

Large release artifacts may use the Artifact Spine Protocol convention:

```text
YYYYMMDD__DOMAIN__TYPE__SCOPE__LINEAGE__SLUG.ext
```

## Notes on addendum numbering

This first pass preserves the existing documents while normalizing their filenames. Affective Signaling and Witness-Readable Controlled Verifiability both appeared as Addendum V in earlier drafts, so this repository temporarily distinguishes them as `addendum-05a` and `addendum-05b` until the canon numbering is finalized.

## Notes on TIS

The Trust Interoperability Standard materials were added in V002 as first-pass Markdown conversions from DOCX source files. This is the right repository for TIS because it functions as the semantic interoperability layer adjacent to HumanKey authentication and Abracadabracadoo consent/proof communication.

## License

Unless otherwise noted, documentation and assets in this repository are made available under the Creative Commons Attribution 4.0 International License. See `LICENSE.md`.

### Ephemeral Trust Papers

A six-part conceptual series on immediate, contextual, revocable trust; portable anchors; consent immune systems; cultural infrastructure; governance/market implications; and trust as resonance. See [`protocols/ephemeral-trust/`](protocols/ephemeral-trust/).


### Loop Training

A six-part training sequence for loop recognition, relational field sensing, structural reflexivity, field identity, substrate awareness, and deployment as consent-coded training tools. See [`protocols/loop-training/`](protocols/loop-training/).
