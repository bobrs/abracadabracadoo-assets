---
title: "Provisional Patent Filing: Abracadabradoo Protocol"
registry_id: "AAP-LEGAL-PROVISIONAL-001"
status: "legal-draft"
category: "legal"
canonical_format: "markdown"
original_status: "Reference Draft"
source_file: "Provisional_Patent_Filing_Abracadabradoo.docx"
---
# Provisional Patent Filing: Abracadabradoo Protocol

## Provisional Patent Filing: Abracadabradoo Protocol – Claims and Supporting Description

## Title

Abracadabradoo Protocol: Nested AEAD Messaging with Server-Mediated Proof Release

## Inventor

**Name:** Bobby Simpson  
**Email:** [<u>uspto@bobbysimpson.com</u>](mailto:uspto@bobbysimpson.com)  
**Date of Conception:** May 5, 2025

## Field of Invention

This invention relates to the field of secure communications, specifically systems and methods for end-to-end encrypted message transmission with server-mediated delivery confirmation using nested authenticated encryption and cryptographic proof tokens.

## Background

Conventional secure messaging protocols rely on mutual trust between parties or server-mediated confirmation of message delivery. These models often require trust in servers or expose metadata. The Abracadabradoo Protocol addresses this limitation by enabling:

- End-to-end encryption between sender and recipient;

- Server-mediated verification without revealing message content;

- Reconstructable, verifiable proof of message receipt;

- Erasable metadata through proof token control.

## Summary of the Invention

The invention provides a cryptographic protocol using:

1.  **Nested AEAD encryption** where the message is encrypted under a nonce derived from the hash of a proof token, and the proof token is encrypted under a nonce derived from the message.

2.  **Server-mediated proof release**, where a server logs only encrypted artifacts and confirms delivery via deterministic, irreversible mappings.

3.  **Post-facto verifiability**, enabling third-party verification that the message was decrypted and obtained by the recipient without ever revealing plaintext to the server.

## Claims (Provisional Draft)

1.  **A method of message encryption and proof binding comprising:**

    - Deriving a proof token from the plaintext message and timestamp using HMAC;

    - Hashing the proof token to produce a nonce for message encryption;

    - Encrypting the message using an AEAD cipher and the derived nonce;

    - Hashing the resulting ciphertext to derive a nonce for encrypting the proof token;

    - Encrypting the proof token using a second AEAD cipher with the second nonce;

    - Transmitting both ciphertexts to a server which logs only the message hash and a timestamp.

2.  **The method of claim 1**, wherein the server responds to a challenge from the recipient by decrypting and releasing the proof token using pre-shared key material.

3.  **The method of claim 1**, wherein the server does not obtain access to plaintext message data or decryption keys.

4.  **The method of claim 1**, wherein the sender and recipient share a first encryption key and the sender and server share a second proof key.

5.  **The method of claim 1**, wherein verification is enabled by any third party holding the encrypted message, proof token, and relevant keys.

6.  **A system for secure message exchange comprising:**

    - A sender device configured to compute and bind proof tokens to encrypted messages using nested AEAD encryption;

    - A server configured to log hashed message identifiers and release encrypted proofs only upon valid challenge submission;

    - A recipient device configured to challenge the server and verify message integrity using received proofs.

7.  **The system of claim 6**, wherein the sender and server utilize non-interactive, append-only logging to ensure tamper-evident message flow.

8.  **The system of claim 6**, wherein deletion of key material or logs renders all proof tokens unrecoverable.

9.  **The system of claim 6**, wherein the nonce derivation strategy uses truncated SHA256 outputs to ensure unique encryption contexts.

10. **The system of claim 6**, wherein nested AEAD allows message and proof linkage without revealing content to intermediaries.

## Supporting Description

The Abracadabradoo Protocol uniquely employs **nested AEAD encryption** that binds a proof token to a message and vice versa through a double-hash chaining scheme. This design enables:

- **Forward secrecy**: once the server has released the proof, it cannot re-generate it without re-access to the key.

- **Ephemerality**: tokens can be set to expire or be deleted, erasing all server-side evidence.

- **Auditability**: third parties can verify that the message was received and decryptable, even without knowing the message content.

By combining deterministic hash-nonce derivation and dual-key control paths (sender↔recipient and sender↔server), the system ensures cryptographic binding between message, proof, and log without exposing the content to the server.

This method is extensible to:

- Legal service (proof of delivery);

- Secure receipts for AI agents;

- Anonymous evidence channels;

- Consent-based audit trails.

## End of Document
