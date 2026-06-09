# Media

Public media assets: videos, social clips, generated diagrams, animations, and launch materials.

## Current media

| File | Role | Notes |
|---|---|---|
| `human-key/HumanKey Explainer.mp4` | HumanKey explainer video | Large binary asset; consider Git LFS or GitHub Releases for long-term repository hygiene. |

## Large-file guidance

For GitHub hygiene, consider one of these approaches as the repository grows:

1. Keep source videos out of git and attach them to GitHub Releases.
2. Store optimized web versions only.
3. Use Git LFS if versioning large media is necessary.

This repository currently includes the HumanKey explainer video because it is a public-facing asset connected to the protocol shelf.


## Large media handling

Large MP4 files are excluded from V007 of the main repository zip. Publish video assets through Git LFS, GitHub Releases, or an external media host and link them from this folder.
