# Docs Review Pass 2 Tier 0-1 Architecture Synthesis

Date: 2026-06-10

Scope: Tier 0 and Tier 1 documents from `docs-review-pass-1-inventory-and-plan.md`, plus a narrow read-only check of the current manual-message shape in the local Abracadoo app folder. No app code or protocol documents were modified.

## 1. Executive summary

V0.8 can still be “manual exchange UX,” but it should not proceed directly from the current V0.7.1 shape. A small V0.7.2 protocol-alignment pass is warranted first.

The needed V0.7.2 is not a rewrite and should not implement the full server-mediated Abracadabracadoo core proof flow. It should make the current app profile honest and migration-friendly:

- add a first-class local `LoopWitness` shape, or at minimum schema-stamped `loop.completed` data, instead of a thin contact-level event
- keep explicit consent confirmation separate from message delivery, receipt, loop witness, and app Relationship status
- reserve manual-message envelope namespaces for future core proof material, controlled verifiability, and conditional deniability without implementing those layers yet
- clarify delete/revoke/archive/forget/backup semantics before UX expands
- remove or sharply scope plaintext-derived event metadata such as `plaintextSha256`

The canon supports this conservative path. `Abracadoo.app` is a reference implementation, not the whole protocol ecosystem ([`docs/stack-map.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/docs/stack-map.md), “Positioning principle”). HumanKey is the relationship-sized authentication layer ([`protocols/README.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/README.md), “HumanKey”). Abracadabracadoo is the communication/proof layer ([`docs/stack-map.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/docs/stack-map.md), “Layer roles”). The current manual exchange can remain an Abracadoo.app HumanKey profile as long as it does not claim to be the full nested-AEAD core spec.

## 2. Immediate decisions before V0.8

1. Public naming should use **Abracadabracadoo** for the ecosystem/protocol family, **Abracadoo.app** for the app/reference implementation, and **HumanKey** for the trust/authentication ontology. `Abracadabradoo`, `Abracadabra`, `DeepTrust`, and `Dialogica` are legacy/provenance names unless a source document is being quoted or cited ([`docs/canon-stewardship-notes.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/docs/canon-stewardship-notes.md), “Naming” and “Legacy project names”).

2. `Acquaintance`, `Path`, `Loop`, and `Relationship` do not conflict with Tier 0/Tier 1 canon if they are documented as **Abracadoo.app profile terms**. They should not be presented as universal Abracadabracadoo protocol terms.

3. TOTP should continue to be described as possession/session authentication, not Relationship proof. The HumanKey draft says TOTP participates in human-mediated mutual authentication and that successful code validation confirms a bounded authentication session ([`protocols/human-key/human-key-mutual-handshake-authentication-rfc-draft.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/human-key/human-key-mutual-handshake-authentication-rfc-draft.md), “Authentication Event”).

4. `Relationship` after sent+received is acceptable only as an app-profile shorthand for “witnessed reciprocal manual exchange.” It must not imply consent to message contents, legal agreement, durable identity, public trust, or human relationship quality. The consent extension explicitly says provable delivery/decryptability does not itself prove reading or consent ([`protocols/extensions/consent-confirmation-loop-extension.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/extensions/consent-confirmation-loop-extension.md), “Motivation”).

5. V0.8 should not add public/broadcast/listening Paths based on Tier 0/Tier 1. Those concepts should wait for a later pass over TIS, CICP, Loopmail, and LOOPtLOOP.

## 3. Must-change app architecture items

1. Introduce a first-class local `LoopWitness` shape before V0.8.

Current `loop.completed` data is too thin for canon alignment because it records contact-level sent/received booleans. Addendum III defines a minimal witness grammar around `loop_id`, `participants`, `consent_flags`, `witness_roles`, `payload_hash`, and `timestamp` ([`protocols/addenda/addendum-03-minimal-witness-structures.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/addenda/addendum-03-minimal-witness-structures.md), “Header Structure: CCL Fields”). V0.7.2 should create a stable local witness object or event payload with at least:

- `schema`: `ABRACADOO_LOOP_WITNESS`
- `schemaVersion`
- `loopId`
- `basis`: `manual_message_exchange`
- `scope`: `path_pair` now, even if a contact-level compatibility view remains
- `contactId`
- `inboundPathId` and `outboundPathId`, when known
- `participants`: local/remote public-key or path-key references, not plaintext identity claims
- `evidence`: sent/received message ids and artifact digests
- `payloadHashes`: ciphertext/artifact hashes, not message plaintext or summaries
- `witnessedAt`
- `witnessRole`: local app as `log` or `verifier`
- optional `consentFlags` with a clear value such as `not_applicable` or `not_claimed` until explicit consent exists

2. Stop treating `relationship.established` as a stronger proof than the evidence supports.

V0.7.2 can keep the event if copy and data make the basis explicit: `basis: witnessed_manual_loop`, `consentToContents: false`, `explicitConsentConfirmation: absent`. A safer UX label is “Loop witnessed” as the primary status, with “Relationship” explained as the app’s witnessed-loop state.

3. Separate consent confirmation from delivery/receipt.

The consent extension creates a subsequent consent declaration `C` tied to a prior message hash and then sends `C` through its own Abracadabracadoo loop ([`protocols/extensions/consent-confirmation-loop-extension.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/extensions/consent-confirmation-loop-extension.md), “Protocol Extension Flow” and “Proof Structure”). V0.7.2 should reserve a status/event such as `consent.confirmed` or `message.consent_confirmed`, but V0.8 manual exchange UX does not need to implement it.

4. Add artifact-envelope reservations without implementing full core proof.

The current manual artifact shape is a valid app profile if it remains clearly named `HK_MANUAL_MESSAGE_1`, but it is not the core Abracadabracadoo nested-AEAD flow. The core spec defines `M`, `P`, `EM`, `EP`, `H_P`, `H_EM`, `msgID`, and server timestamps ([`protocols/core/abracadabracadoo-protocol-specification.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/core/abracadabracadoo-protocol-specification.md), “Terminology” and “Protocol Flow”). V0.7.2 should reserve optional envelope areas:

- `proof`: `mode: none | abracadabracadoo_core | conditional_deniability`
- `coreProof`: optional future slots for `EM`, `EP`, `P`/`pHash`, `hEm`, `proofLogRef`
- `witness`: optional `loopId`, `payloadHash`, `witnessPolicy`
- `controlledVerifiability`: optional `sigBlockRef`, `sigBlockDisclosure`
- `deniability`: optional `recipientProofMode`, `recipientProofRef`

5. Remove or gate plaintext-derived event metadata.

The storage addendum treats encrypted messages as artifacts whose readability depends on keys and warns that forgetting cannot prove no endpoint retained plaintext ([`protocols/addenda/storage-forgetting-addendum.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/addenda/storage-forgetting-addendum.md), “Messages (`EM`) as Artifacts” and “Honest Limitations”). Event logs should keep lifecycle facts, path IDs, message IDs, artifact digests, ciphertext hashes, and witness IDs. They should not keep message contents, summaries, or plaintext hashes by default. A plaintext hash can become an evidentiary capability for guessed low-entropy messages.

## 4. Should-reserve fields/items

1. HumanKey log interoperability fields.

Reserve `session_id`, `role`, `outcome`, and `signature` for trust-log export. The HumanKey draft recommends those fields for optional signed trust logs ([`protocols/human-key/human-key-mutual-handshake-authentication-rfc-draft.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/human-key/human-key-mutual-handshake-authentication-rfc-draft.md), “Log Format”).

2. Revocation message fields.

Map current `credential.revoked`, `path.revoked`/future path revocation, and `contact.revoked` to a future signed revocation object containing sender public key, target session/path/contact hash or ID, timestamp, optional reason, and signature ([`protocols/human-key/human-key-mutual-handshake-authentication-rfc-draft.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/human-key/human-key-mutual-handshake-authentication-rfc-draft.md), “Revocation and Synchronization”).

3. Exchange URI / invite alignment.

Path invites can map cleanly to the HumanKey exchange URI idea: `humankey://exchange?pubkey=...&label=...&expires=...` ([`protocols/human-key/human-key-mutual-handshake-authentication-rfc-draft.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/human-key/human-key-mutual-handshake-authentication-rfc-draft.md), “URI Format for HumanKey Exchanges”). Keep current file/export invites, but reserve `expires`, `label`, and public-key canonicalization fields.

4. Loop-local time fields.

HK_TOTP_1 can remain wall-clock TOTP, but reserve optional `timeProfile`, `epochStart`, `tickInterval`, `driftMargin`, and `epochPrivacy` fields for future loop-local time. Addendum IV defines subjective epochs as mutually initialized, private, non-absolute loop timebases ([`protocols/addenda/addendum-04-loop-local-totp-and-subjective-epochs.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/addenda/addendum-04-loop-local-totp-and-subjective-epochs.md), “Defining the Epoch” and “TOTP Implementation with Subjective Epochs”).

5. Storage state fields.

Reserve lifecycle fields for `active`, `archived`, `revoked`, `forgotten`, and `tombstoned`. The storage addendum distinguishes soft revocation, cryptographic erasure, and verifiable forgetting with tombstones ([`protocols/addenda/storage-forgetting-addendum.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/addenda/storage-forgetting-addendum.md), “Forget Execution Levels” and “Proof of Forgetting”).

## 5. Can-wait items

1. Full Abracadabracadoo core EM/EP/P implementation can wait.

Manual exchange can be a HumanKey app profile for V0.8. Implementing server-mediated proof release, proof-token release, and auditor verification should wait until there is an actual proof server or equivalent local/manual proof design.

2. Witness-readable plaintext shells can wait.

Addendum V-A requires a signature block with `sender_sig`, optional recipient signature, and nonce; verification happens only when the signature block is disclosed ([`protocols/addenda/addendum-05a-witness-readable-controlled-verifiability.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/addenda/addendum-05a-witness-readable-controlled-verifiability.md), “Signature Block Schema” and “Protocol Behavior”). V0.8 should reserve fields, not implement witness-readable plaintext.

3. Conditional deniability crypto can wait.

Addendum VI adds recipient-contributed `K_bobproof`, `Inner_H`, and modified `P` construction ([`protocols/addenda/addendum-06-conditional-deniability.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/addenda/addendum-06-conditional-deniability.md), “Protocol Modification”). V0.8 should not add this unless manual exchange becomes legally/audit-oriented.

4. Full storage/forgetting proofs can wait.

Sparse Merkle trees, signed roots, and third-party Proof of Forgetting are not needed for local MVP. What is needed now is honest semantics and data minimization.

5. Full path-pair Loop entity can wait, but path-pair evidence should not.

Do not build a complete Loop table if it would slow V0.8. Do record path IDs and evidence IDs in the `LoopWitness` so future path-pair modeling is possible without guessing.

## 6. Do-not-implement-yet items

- Public/broadcast/listening Paths. Tier 0/Tier 1 do not require them. Addendum III mentions public/private ledgers as use cases, not as required app primitives ([`protocols/addenda/addendum-03-minimal-witness-structures.md`](https://github.com/bobrs/abracadabracadoo-assets/blob/main/protocols/addenda/addendum-03-minimal-witness-structures.md), “Use Cases”).
- TIS export/import semantics. TIS is important but outside the requested Tier 1 read. Do it in a later TIS-focused pass.
- CICP/Loopmail/LOOPtLOOP carrier and listening concepts. Defer to a later Pass 2 on near-roadmap layers.
- Blockchain/public immutable logs. They would complicate forgetting and deniability before the local model is settled.
- Legal consent/agreement UX. Explicit consent confirmation should be reserved, not implied by message receipt.
- Subjective-epoch TOTP. Reserve fields now; implement later when offline/time-private loops are on the roadmap.

## 7. Proposed V0.7.2 if needed

Yes: add V0.7.2 before V0.8. Keep it small.

V0.7.2 scope:

1. Define and store `ABRACADOO_LOOP_WITNESS` locally.
2. Change `loop.completed` event data to reference the `LoopWitness` ID.
3. Change `relationship.established` data/copy to say it is based on a witnessed reciprocal manual exchange, not consent to content.
4. Add a reserved `consent` status/event namespace, but do not require explicit consent for app Relationship unless the product decision changes.
5. Extend `ABRACADOO_HUMANKEY_MANUAL_MESSAGE` with optional reserved objects for `proof`, `witness`, `controlledVerifiability`, `deniability`, and `timeProfile`, while continuing to accept schema version 1 imports.
6. Stop storing plaintext hashes by default in message events; keep artifact/ciphertext digests.
7. Add user-facing semantics for delete/revoke/archive/forget/backup:
   - delete: remove a local visible copy or record from the current device
   - revoke: mark a Path/credential/contact unusable going forward
   - archive: hide or quiet without claiming cryptographic erasure
   - forget: remove local official capability where possible; do not claim global erasure
   - backup: encrypted export that may preserve capabilities until destroyed
8. Add copy warning that restoring an older encrypted backup can restore keys or records that were later deleted/forgotten locally.

## 8. Green-light criteria for V0.8 manual exchange UX

V0.8 is green-lit when:

- manual message artifacts clearly identify themselves as `HK_MANUAL_MESSAGE_1` / Abracadoo.app profile artifacts, not full Abracadabracadoo core proof artifacts
- every Loop witness has stable evidence references: message IDs, artifact/ciphertext digests, inbound/outbound Path IDs when known, and timestamp
- UI distinguishes TOTP verification, message receipt, loop witness, app Relationship, and explicit consent confirmation
- no copy says receipt means read, agreement, consent, legal acceptance, or permanent nonrepudiation
- event logs avoid plaintext content, plaintext summaries, and plaintext hashes by default
- delete/revoke/archive/forget/backup copy is honest about local capability, keys, backups, and endpoint copies
- Path invite/export fields can later map to HumanKey exchange URI semantics
- wall-clock HK_TOTP_1 remains explicit as the MVP time profile, with no claim of subjective epoch support yet
- public/broadcast/listening Paths are explicitly out of scope for V0.8

## 9. Open questions for human decision

1. Should app `Relationship` continue to mean “witnessed reciprocal exchange,” or should the app introduce `Loop witnessed` as the terminal V0.8 state and reserve `Relationship established` for an explicit user confirmation?

2. Should `LoopWitness` be an event payload only, or a separate artifact/record that can later be exported?

3. Should a recipient’s imported message event ever store a plaintext hash for local integrity/audit, or should that be removed entirely unless the user explicitly creates a proof artifact?

4. Should V0.7.2 bump manual-message schema to version 2, or keep schema version 1 with optional fields and stricter profile wording?

5. Should explicit consent confirmation be a separate manual-message type in V0.8, or deferred until legal/agreement workflows exist?

6. What is the intended public copy for “forget” in a local-first app with encrypted backups: “forget locally,” “remove local access,” or “destroy local key material”?

7. Should archived/revoked/forgotten Paths remain visible in history by default, or should the app support a tombstone-only view?

8. Should loop IDs be deterministic hashes of path-pair/evidence data, random IDs bound to evidence, or both?

9. Should Path invites adopt `humankey://exchange?...` now as an export option, or wait until QR/web introduction work begins?
