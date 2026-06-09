---
title: "The Promise of Abracadabracadoo - Something New in E2EE"
registry_id: "AAP-WHITEPAPER-001"
status: "whitepaper"
category: "whitepapers"
canonical_format: "markdown"
original_status: "Public Explainer"
source_file: "Abracadabracadoo - The Promise of Self-sovereign Privacy.docx"
legacy_name_contains: "DeepTrust"
---
# The Promise of Abracadabracadoo - Something New in E2EE

> **Provenance note:** This document preserves historical naming from earlier drafts. References such as `Abracadabradoo`, `DeepTrust`, or `Dialogica` may indicate legacy project names, source-document context, or sibling protocol material rather than current public positioning.
**The Promise of Abracadabracadoo –  
Something New in E2EE**

## What Is End-to-End Encryption?

End-to-End Encryption (E2EE) is a technique that ensures that only the sender and recipient of a message can read its contents. Whether you're using WhatsApp, Signal, or iMessage, E2EE works by encrypting your messages on your device and decrypting them only on your recipient's device. Not even the server relaying your message can read it.

In simple terms: **E2EE turns your conversation into a locked box where only you and the intended person have the keys.**

## The Current Challenges with E2EE

While E2EE is a major privacy advancement, it still has some gaps:

## 1. Lack of Verifiability

You can’t prove to a third party (or even yourself, after the fact) that someone actually received and decrypted your message. There’s no cryptographic receipt.

## 2. Centralized Trust

Many E2EE systems rely on centralized servers (like Signal or WhatsApp). If the central authority fails or is compromised, your privacy can be at risk.

## 3. Metadata Leakage

While the message content is encrypted, details like who you talk to, when, and how often can still be visible to servers.

## 4. Group Messaging Tradeoffs

Some protocols sacrifice security features like forward secrecy for scalability, especially in group chat scenarios.

## 5. No Built-in Deniability or Erasability

Once a message is delivered, there's often no cryptographic way to make that message provably disappear. Deleting it from your app doesn’t mean it’s gone from the system.

## Enter Abracadabracadoo: A New Kind of E2EE

The **Abracadabracadoo Protocol** is designed to address these limitations by adding a new concept: **cryptographic proof of message receipt**, without sacrificing privacy.

In other words, you can now send a message and later **prove** (without revealing the message) that it was received and decrypted by the recipient.

## How It Works (in Layman's Terms)

- You encrypt your message like normal.

- You also create a "proof token" (think of it as a secret receipt).

- The message and proof token are each encrypted and tied together through cryptographic hashes.

- The server helps log and release the proof, but never sees the actual message.

- If someone ever needs to verify the message was delivered and decrypted, the proof can be checked—**without exposing what was said.**

It’s like having a sealed envelope with a notarized stamp that says, "Yes, this was opened by the right person," without showing what’s inside.

## How Does Abracadabracadoo Compare to Other Protocols?

Here’s how Abracadabracadoo stacks up against current E2EE standards:

| **Feature / Protocol**  | **Abracadabracadoo**                                                 | **Signal**                                        | **Matrix (Olm/Megolm)**                        | **MLS (Messaging Layer Security)**            | **Session**                             |
|-------------------------|----------------------------------------------------------------------|---------------------------------------------------|------------------------------------------------|-----------------------------------------------|-----------------------------------------|
| **Encryption Model**    | Nested AEAD with hash-derived nonces                                 | Double Ratchet + X3DH                             | Olm (1:1) / Megolm (group)                     | TreeKEM-based group key management            | Signal-based (forked)                   |
| **Proof of Receipt**    | Yes (server-mediated release of encrypted proof token)               | No                                                | No                                             | Not inherently; requires audit extensions     | No                                      |
| **Metadata Protection** | High – server never sees plaintext; logs only hashes + timestamps    | Medium – message metadata may be leaked to server | Medium – server sees message routing info      | Medium to High (depending on deployment)      | High – uses onion routing               |
| **Group Messaging**     | Not yet specified                                                    | Supported via Sender Keys (moderate scalability)  | Megolm supports scalable groups                | Native – scalable and efficient               | Supported                               |
| **Decentralization**    | Yes – relies on HumanKey + user-chosen servers                       | No – centralized server infrastructure            | Yes – federation across Matrix homeservers     | Yes – decentralized by design                 | Yes – fully decentralized using Lokinet |
| **Forward Secrecy**     | Yes (ephemeral key + log deletion destroys proof)                    | Yes                                               | Partial – Megolm lacks perfect forward secrecy | Yes – cryptographic trees enable FS           | Yes                                     |
| **Identity Binding**    | HumanKey identities; sender-initiated proof tokens                   | Phone numbers / stable IDs                        | Matrix ID                                      | Group/member credentials                      | Anonymous IDs (public key)              |
| **Deniability**         | Yes – AEAD and ephemeral logs allow plausible deniability            | Yes                                               | Partial                                        | Planned feature                               | Yes                                     |
| **Uniqueness**          | Server-verifiable proof without compromising message confidentiality | Popular for reliability, security                 | Federation and multi-device support            | Future standard for scalable secure messaging | Anonymous, censorship-resistant         |

## Strategic Positioning: Where Abracadabracadoo Shines

## 1. Verifiable Trust Without Exposure

You can prove a message was received and decrypted – without the server or any auditor ever seeing its content. That’s ideal for:

- Digital agreements

- Consent-driven communication

- Regulatory or civic transparency systems

## 2. Ephemerality That Matters

Because proof tokens and keys can be permanently deleted, you get built-in **cryptographic erasure**. Once the logs or keys are gone, there is no way to recover the message – not even by force.

## 3. Transparency-Enabled by Design

Unlike anonymous-focused platforms, Abracadabracadoo is made for accountable dialogue. It fits perfectly into systems like **Dialogica** or **DeepTrust**, where proving what was said (and to whom) is part of the process.

## 4. Extensible Framework

Because it relies on modular components like AEAD ciphers, hash functions, and message IDs, the protocol is easy to adapt to various ecosystems: from WebRTC chats to decentralized social networks.

## 5. HumanKey + Key Sharing = Social-Scale Messaging

The protocol aligns with a world where identities are ephemeral but trust is shared and cryptographically provable. It avoids the surveillance of phone-number-based ID while preserving meaningful connections.

## Real-World Use Cases

## Digital Consent Agreements

In healthcare, education, or employment scenarios, individuals often need to agree to terms or acknowledge important information. Abracadabracadoo allows for provable, private acceptance of terms—where no third party sees the message, but verification is still possible.

## Decentralized Governance

Community members can participate in votes or discussions, and later verify that their encrypted inputs were received and counted without revealing individual contributions.

## Private Contracting

Freelancers and clients can exchange binding agreements or project specs with cryptographic receipts proving who read what and when—without relying on centralized platforms.

## Whistleblower Channels

Journalists and sources can use Abracadabracadoo to exchange secure information, with optional receipt verification, while preserving total content confidentiality and plausible deniability.

## AI-Human Audit Logs

In platforms like Dialogica, every AI response or suggestion can be backed with a verifiable message receipt, enabling a new level of traceability in automated decision-making.

## Final Thoughts

E2EE got us part of the way to private, secure communication. **Abracadabracadoo picks up where those protocols left off**, adding auditability, erasability, and user-sovereign proof into the mix.

In a world where trust must be built and verified – without compromising privacy – Abracadabracadoo is not just another messaging protocol.

## It's a new category.
