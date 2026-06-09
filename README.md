# Codex Plugin Creator

> Deterministic, local-first scaffolding and manifest validation for Codex plugins.

`codex-plugin-creator` is a clean, public extraction of a working `plugin-creator` skill for Codex. It helps you build and test local Codex plugins reliably by codifying directory shape rules and manifest contracts into a repeatable workspace script.

![Preview](assets/preview.svg)

## Why It Exists

Codex plugin development can fail silently due to subtle packaging errors. A plugin might not load or run because of:

- incorrect directory structure, such as a missing or misplaced `.codex-plugin/` directory
- malformed manifest fields or non-semver version strings in `plugin.json`
- mismatched marketplace registration keys that prevent local loading
- leftover placeholders such as `[TODO: ...]` in skills or descriptions

This tool makes plugin setup deterministic, keeping standard structures and validation contracts local to your workspace.

## What You Get

- `SKILL.md`: the installable Codex skill configuration
- `scripts/create_basic_plugin.py`: scaffold a plugin root and optional marketplace entry
- `scripts/validate_plugin.py`: validate the generated plugin against the expected manifest contract
- `scripts/read_marketplace_name.py`: print the marketplace name Codex expects for reinstall commands
- `scripts/update_plugin_cachebuster.py`: bump a local plugin to a single `+codex.<token>` suffix for reloads
- `references/plugin-json-spec.md`: exact sample shapes and field reference notes
- `references/installing-and-updating.md`: the local update/reinstall loop for existing plugins
- `agents/openai.yaml`: Codex skill metadata
- `assets/preview.svg`: process preview diagram

## Quick Start

### 1. Install to your local Codex skills

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R codex-plugin-creator "${CODEX_HOME:-$HOME/.codex}/skills/plugin-creator"
```

### 2. Scaffold a new plugin

From the installed skill directory:

```bash
python3 scripts/create_basic_plugin.py my-plugin --with-marketplace
```

### 3. Validate before ingestion

```bash
python3 scripts/validate_plugin.py "$HOME/plugins/my-plugin"
```

By default this creates:

- `~/plugins/my-plugin`
- `~/.agents/plugins/marketplace.json`

## Example Output

Running:

```bash
python3 scripts/create_basic_plugin.py demo-plugin \
  --with-skills --with-scripts --with-assets --with-marketplace
```

Produces a plugin like:

```text
~/plugins/demo-plugin/
  .codex-plugin/plugin.json
  skills/
  scripts/
  assets/
```

And adds a marketplace entry at:

```text
~/.agents/plugins/marketplace.json
```

## Updating An Existing Local Plugin

When the plugin already exists and you just need Codex to pick up a new local version:

```bash
python3 scripts/update_plugin_cachebuster.py "$HOME/plugins/demo-plugin"
python3 scripts/read_marketplace_name.py
codex plugin add demo-plugin@personal
```

For repo-local or non-default marketplace paths, use:

```bash
python3 scripts/read_marketplace_name.py --marketplace-path <path-to-marketplace.json>
```

The full local iteration flow is documented in
`references/installing-and-updating.md`.

## Validation Notes

The bundled validator checks for:

- missing `.codex-plugin/plugin.json`
- invalid JSON
- unsupported manifest fields
- non-semver versions
- missing interface metadata
- broken asset paths
- leftover `[TODO: ...]` placeholders

The scaffold and update helpers also keep the marketplace path and cachebuster flow consistent
with current Codex local-plugin behavior.

## Security And Privacy

This public extraction does not include API keys, OAuth material, cookies, browser profiles, local session data, synced private notes, or maintainer-specific project state.

The default scaffold targets generic local paths like `~/plugins` and `~/.agents/plugins/marketplace.json`. Those are defaults used by the tool, not personal machine identifiers.

## License

Apache-2.0
