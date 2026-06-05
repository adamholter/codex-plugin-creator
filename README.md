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
- `references/plugin-json-spec.md`: exact sample shapes and field reference notes
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

## Validation Notes

The bundled validator checks for:

- missing `.codex-plugin/plugin.json`
- invalid JSON
- unsupported manifest fields
- non-semver versions
- missing interface metadata
- broken asset paths
- leftover `[TODO: ...]` placeholders

## Security And Privacy

This public extraction does not include API keys, OAuth material, cookies, browser profiles, local session data, synced private notes, or maintainer-specific project state.

The default scaffold targets generic local paths like `~/plugins` and `~/.agents/plugins/marketplace.json`. Those are defaults used by the tool, not personal machine identifiers.

## License

Apache-2.0
