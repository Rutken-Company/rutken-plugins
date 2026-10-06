# Contributing a plugin

Thanks for contributing a detection to Rutken. Plugins are **declarative matcher
data**, never code.

## Steps

1. Read the authoring guide: <https://www.rutken.com/docs/writing-a-plugin.html>
   (the pack schema, the full matcher grammar, how to use Rutken's own output to
   find what to match, and the taint source/sink catalog).
2. Install Rutken: `curl -fsSL https://www.rutken.com/install.sh | bash`
3. Fork this repo and create a branch.
4. Copy `packs/example.json` to `packs/<publisher>-<id>.json` and edit it:
   - a unique `publisher` and `id`,
   - a `version` (start at `1.0.0`),
   - your `author` name — this is the credit shown on the website,
   - your matcher rules.
5. Validate locally — this is exactly what CI runs:
   ```
   rutken packs validate packs/<your-file>.json
   ```
6. Open a pull request. The **validate** check must be green before review.
7. A maintainer reviews. On approval the pack is merged, credited to you, and
   published to the signed registry.

## What makes a good pack

- **Additive.** It detects something the built-in rules do not already cover, or
  sharpens a generic built-in into a named, attributed detection.
- **Precise.** Low false positives — matcher rules grounded in real APIs and
  concrete signals, not broad guesses.
- **Accurate.** Correct `severity`/`confidence` and a real CWE / MASVS taxonomy.
- **Focused.** One logical detection area per pack.

## Rules of the road

- A plugin is matcher **data**, never executable code.
- Do not submit packs crafted to target a specific person or app maliciously.
- By opening a PR you agree your pack may be published to the Rutken registry
  with credit to the `author` you set.

## How review and publishing work

Your PR adds data to a public repo. CI validates its schema and grammar. A
maintainer reviews it by hand. Only after a maintainer merges does Rutken's
signing pipeline — whose key lives in Azure Key Vault and is never exposed —
sign the pack and publish it to the registry Blob. The signature, verified by
every Rutken client against a pinned key, is what establishes trust; the repo
and the Blob are untrusted inputs to that pipeline.
