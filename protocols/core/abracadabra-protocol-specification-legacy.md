---
title: "Abracadabra Protocol Specification"
registry_id: "AAP-LEGACY-001"
status: "legacy"
category: "core"
canonical_format: "markdown"
original_status: "Legacy Reference"
source_file: "Abracadabra_Protocol_Specification.docx"
---
# Abracadabra Protocol Specification

**Version:** 1.0  
**Date:** April 22, 2025

## 1. Overview

The **Abracadabra Protocol** is a two-layer, server-mediated, end-to-end encryption scheme with embedded hash-based challenge–response. It ensures that a sender (A) can prove delivery and decryption capability by a recipient (B) using only the original file and server logs, without requiring direct recipient confirmation.

## 2. Terminology

- **A**: Sender (Alice)

- **B**: Recipient (Bob)

- **S**: Server (or multi-hop S1, S2)

- **F**: Original file or payload

- **K_AB**: Symmetric key shared between A and B (inner layer)

- **K_AS**: Symmetric key shared between A and S (outer layer)

- **C_inner**: Ciphertext of F under K_AB (C_inner = Enc\_{K_AB}(F))

- **h**: SHA-256 hash of C_inner (h = H(C_inner))

- **C_outer**: Encryption of C_inner under K_AS (C_outer = Enc\_{K_AS}(C_inner))

- **C_locked**: Encryption of C_outer under key h (C_locked = Enc\_{h}(C_outer))

- **msgID**: Unique message identifier

- **T1**, **T2**: Timestamps logged at server receive and challenge events

## 3. Protocol Flow

### 3.1 Preparation and Key Establishment

1.  **Inner Key (A↔B)**: A and B agree on K_AB via any authenticated key-exchange (e.g., double-ratchet).

2.  **Outer Key (A↔S)**: A and S share K_AS through a separate key-exchange or pre-provisioned secret.

### 3.2 Message Encryption and Upload

1.  **Encrypt Inner Layer**:  
    C_inner = Enc\_{K_AB}(F)

2.  **Compute Hash**:  
    h = H(C_inner) (SHA-256)

3.  **Encrypt Outer Layer**:  
    C_outer = Enc\_{K_AS}(C_inner)

4.  **Upload to Server**:  
    A sends (msgID, C_outer) to S.  
    **S logs**: (msgID, h, T1)

5.  **Server Locks**:  
    S computes C_locked = Enc\_{h}(C_outer) and forwards (msgID, C_locked) to B.

### 3.3 Recipient Unlock Challenge

1.  **B Receives**:  
    B obtains (msgID, C_locked) but cannot decrypt without h.

2.  **Challenge Calculation**:  
    B computes h' = H(C_locked) or extracts h via known function.

3.  **Challenge Submission**:  
    B sends (msgID, h') to S.

4.  **Server Verification**:  
    S verifies h' == h.  
    **S logs**: (msgID, h, T2)

5.  **Hash Release**:  
    S returns h to B.

### 3.4 Final Decryption

1.  **Unlock Outer Layer**:  
    C_outer = Dec\_{h}(C_locked)

2.  **Decrypt Inner Layer**:  
    F = Dec\_{K_AS}(C_outer)

3.  **Deliver File**:  
    B now recovers original file F.

## 4. Proof of Delivery and Decryption Capability

At any point, A can demonstrate that B had the ability to decrypt by presenting:

1.  **Original file F** (recomputable C_inner).

2.  **K_AB** (to derive C_inner).

3.  **Server log entries**:

    - (msgID, h, T1) showing receipt of the message.

    - (msgID, h, T2) showing successful challenge by B.

Because h = H(C_inner), the server log ties A’s original file to B’s ability to compute the correct hash, proving decryption capability.

## 5. Security Properties

- **End-to-End Encryption**: Only A and B can decrypt the payload. Servers see only ciphertexts and hashes.

- **Proof without Recipient Signature**: Server-mediated logs replace direct receipts, preserving deniability to third parties.

- **Ephemeral Proof**: Once A and server logs are deleted, no evidence remains.

## 6. Implementation Notes

- Use **AES-GCM** or equivalent AEAD for Enc and Dec functions.

- Use **SHA-256** for hashing.

- Ensure secure random generation for msgID and any nonces.

- Protect server logs in an append-only, tamper-evident store.

## End of Specification
