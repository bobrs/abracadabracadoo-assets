# HumanKey

HumanKey is the relationship-sized authentication layer of the Abracadoo ecosystem.

It treats trust as something closer to a handshake than a monolithic wallet: reciprocal, isolated, and scoped to a particular relationship.

## Current status

HumanKey is live in beta inside Abracadoo.app.

## Core idea

Every relationship gets its own small trust container. A compromise in one relationship should not automatically compromise the rest of a person's identity graph.

## Related implementation

- Abracadoo.app beta: <https://abracadoo.app>
- Working code repo: <https://github.com/bobrs/abracadoo-code>

## Media

Large HumanKey explainer/ad videos are intentionally not included in this first-pass zip to keep the repository lightweight. Add them later under `media/humankey/` or attach them as GitHub release assets.

## Protocol drafts

Canonical Markdown drafts live in `protocols/human-key/`.

- `human-key-mutual-handshake-authentication-rfc-draft.md`
- `human-key-double-totp-legacy-draft.md`
