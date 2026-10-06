# Rutken plugins

Community rule packs for [Rutken](https://www.rutken.com) — declarative security
detections anyone can write, submit, and get credited for.

A "plugin" is **data, not code**: a JSON manifest of matcher rules the Rutken
engine runs through its normal analysis pipeline. A pack never executes on a
user's device — that is the security model. A maintainer reviews every
submission, and only then does Rutken's signing pipeline (its key held in Azure
Key Vault) sign and publish it. A pull request on its own can never get a signed
pack onto anyone's machine.

## Use a published pack

```
rutken packs update  --url https://www.rutken.com/registry
rutken packs install rutken/<id>
```

Browse the catalog at <https://www.rutken.com/plugins.html>.

## Write and submit one

Full guide: **[Writing a Rutken plugin](https://www.rutken.com/docs/writing-a-plugin.html)**
(the pack schema, the matcher grammar, how to find what to match, and the taint
source/sink catalog).

In short:

1. Install Rutken: `curl -fsSL https://www.rutken.com/install.sh | bash`
2. Fork this repo.
3. Copy [`packs/example.json`](packs/example.json) to `packs/<publisher>-<id>.json`
   and edit it (set a unique `publisher`/`id`, a `version`, your `author` name —
   you will be credited — and your matcher rules).
4. Validate locally: `rutken packs validate packs/<your-file>.json`
5. Open a pull request. The **validate** check must pass.
6. A maintainer reviews, approves (crediting you), and the signed pipeline
   publishes it — it then appears on the website and installs via the CLI.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the details and what makes a good pack.
