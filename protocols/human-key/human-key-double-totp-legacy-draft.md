---
title: "Human Mediated Mutual Authentication Negotiated Key Exchange"
registry_id: "HK-LEGACY-001"
status: "legacy"
category: "human-key"
canonical_format: "markdown"
legacy_name_contains: "DeepTrust"
---
# Human Mediated Mutual Authentication Negotiated Key Exchange

> **Provenance note:** This document preserves historical naming from earlier drafts. References such as `Abracadabradoo`, `DeepTrust`, or `Dialogica` may indicate legacy project names, source-document context, or sibling protocol material rather than current public positioning.
Internet Engineering Task Force (IETF) B. Simpson Internet-Draft C. Simpson Intended status: Standards Track DeepTrust Project Expires: October 29, 2025 April 29, 2025

Human Mediated Mutual Authentication Negotiated Key Exchange

draft-simpson-human-double-totp-00

Abstract

This document specifies a simplified protocol for mutual, human-mediated authentication between two parties using Time-based One-Time Passwords (TOTP) and asymmetric cryptographic key exchanges. The protocol explicitly requires human mediation both during the initial key exchange and at authentication time, ensuring secure, human- centric authentication without relying on persistent online connectivity or centralized identity authorities.

Status of This Memo

This Internet-Draft is submitted in full conformance with the provisions of BCP 78 and BCP 79.

Internet-Drafts are working documents of the Internet Engineering Task Force (IETF). Note that other groups may also distribute working documents as Internet-Drafts. The list of current Internet-Drafts is at [<u>https://datatracker.ietf.org/drafts/current/</u>](https://datatracker.ietf.org/drafts/current/).

Internet-Drafts are draft documents valid for a maximum of six months and may be updated, replaced, or obsoleted by other documents at any time. It is inappropriate to use Internet-Drafts as reference material or to cite them other than as "work in progress."

This Internet-Draft will expire on October 29, 2025.

Copyright Notice

Copyright (c) 2025 IETF Trust and the persons identified as the document authors. All rights reserved.

This document is subject to BCP 78 and the IETF Trust's Legal Provisions Relating to IETF Documents ([<u>https://trustee.ietf.org/license-info</u>](https://trustee.ietf.org/license-info)) in effect on the date of publication of this document. Please review these documents carefully, as they describe your rights and restrictions with respect to this document.

Table of Contents

1.  Introduction

> As identity spoofing and impersonation threats continue to grow, especially in remote or low-connectivity environments, new approaches are needed for mutual authentication that place trust back into the hands of individuals. This document describes a lightweight, decentralized authentication protocol that combines Time-based One-Time Passwords (TOTP) with human mediation at two critical junctures: the initial cryptographic key exchange, and each real-time authentication event.
>
> The protocol provides peer-to-peer authentication that avoids institutional or cloud-based intermediaries, allowing users to establish and validate trust directly. It leverages asymmetric cryptography to securely exchange per-relationship secrets, and requires both parties to actively participate in the verification process using human communication channels such as phone or video.
>
> In environments where connectivity is intermittent or fully offline, the protocol supports deferred log synchronization and maintains verifiable logs of all trust events. These characteristics make it suitable for secure interpersonal authentication across civil, operational, and field settings.
>
> Human relationships are inherently dynamic: bonds may strengthen, weaken, or reemerge across time and context. The HumanKey protocol embraces this natural flexibility by enabling a persistent cryptographic relationship whose trust state is inherently ephemeral and human-mediated. Much like an elastic thread woven into fabric, HumanKey provides subtle elasticity in the structure of interpersonal digital trust — allowing it to stretch, tighten, or relax without breaking. It supports durable memory of prior trust while permitting effortless revalidation or graceful expiration, aligned with the humans’ own choices rather than institutional dictates. This architecture restores autonomy, adaptability, and direct agency to participants in digital authentication.
>
> **Identity is what’s presented**; **trust is what’s granted in response**.
>
> But in **HumanKey**, these are fused: Your *persistent keypair* is an identity anchor. Your *TOTP code exchange* activates trust. When both are human-mediated and optionally time-bound, the system supports **ephemeral trust**, and **pseudo-ephemeral identity**.
>
> By **not binding identity to an institution**, HumanKey enables a kind of **super-self-sovereign, elastic identity** that can:

- Persist for decades *or*

- Be dropped tomorrow with no external trace

> This creates a space where **identity itself can be ephemeral**, **revocable**, and **unlogged**, unless humans choose to retain or synchronize it.

2.  Terminology

> The following terms are used throughout this document:

- **Ephemeral Trust:** A persistent cryptographic relationship whose active trust state is subject to voluntary, human-mediated revalidation. While the underlying keys may persist indefinitely, the trust they enable adapts dynamically—expiring, renewing, or reawakening based on human behavior rather than automated systems. This mirrors the flexible, durable, and sometimes dormant nature of human relationships.

- **Ephemeral Identity:** A temporary, context-specific digital persona formed through the presentation of a unique keypair and voluntary interaction. While a keypair may persist, the identity it represents is not inherently linked to a broader account or institution, allowing individuals to present themselves anew in each relationship. Ephemeral identity supports privacy, minimization, and human-centered negotiation of recognition.

- **Initiator**: The party who begins the authentication process or initiates a relationship request.

- **Responder**: The party who receives a request to authenticate or form a relationship.

- **TOTP (Time-based One-Time Password)**: A short-lived code generated from a shared secret and the current time, as specified in RFC 6238.

- **Public Key / Private Key**: Asymmetric keypair used to encrypt and decrypt the TOTP secret during initial key exchange.

- **Human-Mediated Channel**: Any trusted, real-time communication medium between users, such as a phone call, video call, or in-person meeting.

- **Authentication Session**: A bounded time window during which two parties confirm each other’s identities using shared TOTP codes.

- **Local Trust Log**: A secure, timestamped record of authentication and trust events, retained on the user’s device.

3.  Protocol Description

3.1. Initial Key Exchange (Human-Mediated)

To begin a secure relationship, the Initiator (User A) generates a new asymmetric keypair unique to their interaction with the Responder (User B).

1.  **Key Generation**: User A creates a public/private keypair for use exclusively in the relationship with User B.

2.  **Public Key Sharing**: Using a human-mediated channel (e.g., voice call, in-person meeting), User A provides their public key to User B.

3.  **TOTP Secret Generation**: User B generates a new TOTP secret specific to User A.

4.  **Secret Encryption**: User B encrypts the TOTP secret with User A's public key.

5.  **Secret Transmission**: Via the same human-mediated channel, User B transmits the encrypted TOTP secret to User A.

6.  **Secret Decryption**: User A uses their private key to decrypt and store the secret.

This process is then repeated in reverse, enabling both parties to hold a TOTP secret created by the other. Each party thus gains the ability to validate the TOTP codes generated by their counterpart.

3.2. Authentication Event (Human-Mediated)

Once a mutual relationship is established and both parties hold TOTP secrets generated by the other, authentication can be performed as needed using human-mediated communication.

1.  **Session Initiation**: Either user (Initiator or Responder) proposes an authentication session through a real-time human channel such as a phone or video call.

2.  **Code Generation**: Each user uses the TOTP secret they received during key exchange to generate a current code.

3.  **First Exchange**: User A verbally communicates their generated TOTP code to User B.

4.  **First Validation**: User B manually enters the received code into their device and validates it against the expected value.

5.  **Second Exchange**: User B then communicates their own TOTP code to User A.

6.  **Second Validation**: User A manually enters and validates the code.

If both codes are validated successfully, mutual authentication is confirmed. The result may optionally be recorded in the local trust logs and considered valid for a predefined duration (e.g., 5 minutes).

3.3. Offline Operation and Logging

The protocol is designed to function even when no internet or centralized infrastructure is available. Users may perform mutual authentication offline by leveraging previously exchanged TOTP secrets.

1.  **Cached Secrets**: Each party stores the TOTP secrets locally on their device.

2.  **Manual Session**: Authentication proceeds as normal using a phone call or in-person exchange, with each party generating and validating TOTP codes.

3.  **Event Logging**: Each device logs the authentication event with a timestamp, directionality (who initiated), and validation results.

4.  **Deferred Sync**: When connectivity is restored, logs can be uploaded and merged with a central or shared trust record. Cryptographic signatures ensure consistency and prevent tampering.

This offline capability supports robust use in low-resource, high-security, or field settings where connectivity is unreliable or delayed.

4.  Optional Extensions

> This section outlines enhancements to the core protocol that may be implemented to improve flexibility, session control, and lifecycle management.

1.  **Session Duration Customization**: Authenticated sessions may allow custom durations beyond the default (e.g., extend to 30 minutes) if both users consent.

2.  **Manual Session Termination**: Either user can terminate an active session at any time, prompting immediate expiration of mutual trust.

3.  **Trust Revocation Mechanism**: Users can revoke trust relationships individually or globally by issuing signed revocation messages. These can be propagated upon next sync.

4.  **Session Metadata**: Users may optionally include structured metadata with authentication sessions (e.g., purpose, location, tags), appended to local logs.

5.  **Audit Hooks and Export**: Implementations may support exporting signed trust logs for third-party audit or integration with external security infrastructure.

<!-- -->

5.  Auditable Record

> Every authentication event, whether online or offline, is logged locally by each participant in a tamper-evident format. These logs include:

- Timestamp of the authentication event.

- Role of the user (Initiator or Responder).

- Result of each TOTP validation step (success or failure).

- Optional metadata (if supported and enabled).

> Local trust logs are cryptographically signed to ensure integrity and can be verified upon synchronization or audit. When connectivity becomes available, these logs can be merged with a shared repository, enabling:

- Reconciliation of mutual records.

- Dispute resolution and forensic analysis.

- Rebuilding a verifiable trust graph across relationships.

> Audit transparency is a core design goal. Each log entry serves as a cryptographically provable assertion of interaction, supporting trust without institutional oversight.

6.  Security Considerations

> This protocol assumes the integrity and authenticity of the human-mediated communication channel used for key exchange and TOTP code sharing. Any compromise of this channel (e.g., social engineering, man-in-the-middle attacks during verbal exchange) could lead to impersonation or key leakage.
>
> To mitigate risks:

- Users should confirm identities via secondary trusted methods before accepting keys or TOTP codes.

- Devices must securely store keys and secrets, and restrict access to trust logs.

- TOTP codes are ephemeral by design, limiting the window of exploitation.

- Cryptographic signing of all logs ensures tamper detection.

> The protocol deliberately omits automated validation or reliance on centralized authorities, trading scalability for trust rooted in human verification. Implementers must ensure proper user interface design and user education to prevent misinterpretation or misuse.

7.  IANA Considerations

> This memo includes no request to IANA.

8.  References

> \[RFC6238\] M'Raihi, D., Machani, S., Pei, M., and J. Rydell, "TOTP: Time-Based One-Time Password Algorithm", RFC 6238, DOI 10.17487/RFC6238, May 2011, [<u>https://www.rfc-editor.org/info/rfc6238</u>](https://www.rfc-editor.org/info/rfc6238).

Authors' Addresses

Bobby Simpson DeepTrust Project 601 South Broadway Shawnee, OK 74801 United States

Email: [<u>openai@bobbysimpson.com</u>](mailto:openai@bobbysimpson.com)

Campbell Simpson DeepTrust Project 1441 NW 92nd Street Oklahoma City, OK 73114 United States

Email: [<u>campbell@deeptrust.com</u>](mailto:campbell@deeptrust.com)

---

_Source converted from `Broken Human-Mediated_Double-TOTP_Full_Draft.docx` for repository publication. Markdown is a first-pass canonicalization and may be revised._
