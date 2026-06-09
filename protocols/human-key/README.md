# HumanKey

HumanKey is the relationship-sized authentication layer for the Abracadabracadoo / Abracadoo.app ecosystem.

It centers human-mediated mutual authentication: two parties establish per-relationship cryptographic material, then re-authenticate through short human-exchanged codes such as TOTP values. The goal is trust that can persist, expire, revive, or be discarded at the scale of a real relationship rather than a monolithic identity wallet.

## Current files

| File | Role | Status |
|---|---|---|
| `human-key-mutual-handshake-authentication-rfc-draft.md` | Current HumanKey Internet-Draft style specification | Active draft |
| `human-key-double-totp-legacy-draft.md` | Earlier HumanKey / double-TOTP draft | Legacy reference |

## Implementation status

HumanKey is live in the Abracadoo.app beta.

## Related implementation

<https://github.com/bobrs/abracadoo-code>
