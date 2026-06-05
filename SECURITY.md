# Security Notes

`codex-plugin-creator` is a local scaffolding and validation tool. It does not require API keys, OAuth tokens, browser profiles, or remote services to work.

## Safe Defaults

- The default plugin output path is `~/plugins/<plugin-name>`.
- The default marketplace path is `~/.agents/plugins/marketplace.json`.
- Generated plugin metadata uses placeholder author values such as `Local developer`.

## Before You Share A Generated Plugin

- review `.codex-plugin/plugin.json` for real names, URLs, and descriptions
- remove any local-only scripts, secrets, or private assets you added after scaffolding
- avoid committing marketplace files that include private plugin paths you do not want to publish

## Reporting

If you find a security issue in this public extraction, open a private security advisory or contact the maintainer directly before publishing full details.
