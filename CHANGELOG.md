# Changelog

## 0.1.3

- Reject path-like values passed as the first scaffold argument and point callers to `--path` instead of silently normalizing filesystem paths into plugin names.
- Tightened the README opening around the local scaffold -> validate -> reload loop.
- Reworked `assets/preview.svg` into a simpler black-and-white share graphic grounded in the real commands this repo exposes.

## 0.1.2

- Synced the public extraction with the latest local skill behavior.
- Added `scripts/read_marketplace_name.py` and `scripts/update_plugin_cachebuster.py`.
- Added `references/installing-and-updating.md` plus README coverage for the local update loop.

## 0.1.1

- Polished the public README headline and opening section for a cleaner social-share screenshot.
- Added `SECURITY.md` with guidance on safe defaults and what to review before sharing generated plugins.
- Refined the preview SVG font fallbacks to render more consistently across machines.

## 0.1.0

- Initial public extraction of the `plugin-creator` Codex skill.
- Included the scaffold and validation scripts plus the manifest reference.
- Rewrote internal usage examples to public repo-relative commands.
- Added a truthful preview diagram and public README.
