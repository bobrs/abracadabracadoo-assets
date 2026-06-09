---
title: "Abracadabradoo Protocol Addendum IV: Loop-Local TOTP and Subjective Epochs"
registry_id: "AAP-ADD-04"
status: "draft"
category: "addenda"
canonical_format: "markdown"
original_status: "Time-Unbound Operational"
source_file: "Abracadabracadoo_Protocol_Addendum IV.docx"
---
# Abracadabradoo Protocol Addendum IV: Loop-Local TOTP and Subjective Epochs

## Status: Time-Unbound Operational
## Filed under: Rhythmic Autonomy and Temporal Consent

## Abstract

This addendum introduces support for **loop-local timebases**—subjective, consent-initialized epochs that allow Time-Based One-Time Password (TOTP) synchronization within semantic loops without relying on global clocks or external entropy. By anchoring loop behavior in negotiated rhythm rather than universal chronology, this mechanism enables resilient, sovereign synchronization across asynchronous, disconnected, or temporally diverse environments.

## 1. The Need for Loop-Local Time

Global time synchronization introduces:

- Centralized dependency (e.g., NTP, GPS)

- Fragility in partitioned networks

- A false assumption of shared reality

SCT-based communication systems require:

- Consent-based reference points

- Forgiveness of drift

- Reconstructable or discardable time semantics

Loop-local epochs allow parties to agree on "now" and count from there.

## 2. Defining the Epoch

Each loop (Diad, Triad, or Group Loop) may negotiate:

- **Epoch start**: a mutual declaration (manual or triggered)

- **Tick rate**: e.g., seconds, pulses, iterations

- **Drift margin**: acceptable deviation window for collapse checks

This epoch is:

- Not shared outside the loop

- Not absolute

- Private unless disclosed

## 3. TOTP Implementation with Subjective Epochs

A traditional TOTP scheme might use:

TOTP(t = UNIX time)

With this addendum:

TOTP(t = seconds_since_loop_epoch)

Where:

- t is derived from local clock since epoch initiation

- The epoch value is initialized by mutual consent

- The TOTP function remains otherwise unchanged

Participants may store:

- epoch_start_timestamp

- shared_secret

- tick_interval

## 4. Synchronization Behavior

- Initial loop establishment includes negotiation of timing

- Collapse logic checks for proximity within allowed drift

- If desynchronized, agents may renegotiate or reset the epoch

This avoids need for external time coordination and supports:

- Offline interactions

- Dynamic rekeying

- Time-private exchanges

### 4.1 Temporal Privacy via Subjective Epochs

Because the epoch and tick rate are known only within the loop, a participant may produce proof of:

- Successful collapse

- Valid synchronization

- Agreement with another agent

Without revealing:

- The real-world time the event occurred

- The duration since loop inception

- Any external or absolute chronology

This enables **provable presence without timestamp leakage**, supporting high-integrity consent without compromising contextual privacy.

The proof reveals nothing about when. Only that it *was.*

- Initial loop establishment includes negotiation of timing

- Collapse logic checks for proximity within allowed drift

- If desynchronized, agents may renegotiate or reset the epoch

This avoids need for external time coordination and supports:

- Offline interactions

- Dynamic rekeying

- Time-private exchanges

## 5. Use Cases

- Secure communications between mobile, disconnected agents

- Protocol loops operating behind firewalls, air gaps, or isolated environments

- Human-mediated rituals requiring local rhythm rather than network precision

## 6. Conclusion

By removing global time as a dependency and treating time as a loop-internal rhythm, this addendum restores autonomy, redundancy, and semantic sovereignty to synchronous verification.

Time is not what the world says it is.  
Time is what we agree it meant—starting *now*.

*Filed under temporal minimalism and loop-centric coordination.*
