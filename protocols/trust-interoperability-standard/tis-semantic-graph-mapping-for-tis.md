---
title: "Semantic Graph Mapping for TIS"
registry_id: "TIS-TIS-SEMANTIC-GRAPH-MAPPING-FOR-TIS"
status: "draft"
category: "trust-interoperability-standard"
canonical_format: "markdown"
---
# Semantic Graph Mapping for TIS

## Purpose

This profile defines how Trust Object Archetypes (TOAs) can be expressed as **semantic linked data** for interoperability, indexing, and reasoning across ecosystems. It enables TIS-defined trust interactions to be queried, composed, and validated using graph-native tools like SPARQL, RDF, and JSON-LD.

## Design Principles

- **Interoperable**: Use standards-compliant vocabularies and JSON-LD context definitions.

- **Modular**: Map fields to reusable ontologies wherever possible (e.g. W3C VC, schema.org).

- **Queryable**: Support graph search and semantic inference.

- **Composable**: Enable linkage between identities, TOAs, credentials, dialogues, and contexts.

## JSON-LD Context Template

{

"@context": {

"archetype_id": "https://trustinterop.org/ontology#archetype_id",

"name": "http://schema.org/name",

"summary": "http://schema.org/description",

"exchange_method": "https://trustinterop.org/ontology#exchange_method",

"consent_mode": "https://trustinterop.org/ontology#consent_mode",

"temporal_profile": "https://trustinterop.org/ontology#temporal_profile",

"cryptographic_basis": "https://trustinterop.org/ontology#cryptographic_basis",

"trust_range": "https://trustinterop.org/ontology#trust_range",

"traceability": "https://trustinterop.org/ontology#traceability",

"revocability": "https://trustinterop.org/ontology#revocability",

"related_archetypes": {

"@id": "https://trustinterop.org/ontology#related_archetypes",

"@type": "@id"

},

"identity": "https://identity.foundation/context#identity",

"extensions": "http://www.w3.org/2000/01/rdf-schema#seeAlso"

}

}

## Sample RDF Triples (Turtle Syntax)

@prefix tis: \<https://trustinterop.org/ontology#\> .

@prefix schema: \<http://schema.org/\> .

\<urn:toa:spirit-link.v1\>

a tis:TrustObjectArchetype ;

schema:name "SpiritLink" ;

schema:description "Embodied ritual-based ephemeral trust" ;

tis:consent_mode "symbolic" ;

tis:temporal_profile "ephemeral" ;

tis:cryptographic_basis "none" ;

tis:traceability "none" ;

tis:trust_range "symbolic" ;

tis:related_archetypes \<urn:toa:phrase-pair.v1\> .

## Use Cases

- **Discovery**: Searchable registries of TOAs by consent type, duration, or cryptographic basis

- **Reasoning**: Infer compatibility between TOAs based on shared modalities

- **Auditing**: Link trust events across dialogues and agents using semantic identifiers

- **Mapping**: Bridge TIS to DIDComm, W3C VC, and identity vocabularies

## Integration Targets

- [<u>schema.org</u>](https://schema.org)

- [<u>DID Specification Registries</u>](https://identity.foundation/)

- [<u>W3C Verifiable Credentials</u>](https://www.w3.org/TR/vc-data-model/)

- JSON-LD Playground

- [<u>SPARQL query services</u>](https://www.w3.org/TR/sparql11-query/)

## Next Steps

- Define canonical @context for TIS archetypes

- Publish TOAs as JSON-LD documents alongside YAML/Markdown

- Create a SPARQL endpoint or TOA Graph Explorer UI

- Integrate with agent frameworks (e.g., Veramo, Ceramic, SpruceID)

---

_Source converted from `Semantic Graph Mapping for TIS.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
