# Gateway Starter

A Paperclip organization package that creates a company whose CEO is already
connected to the OpenCode gateway. Importing it does **not** ask you to connect
a Claude or OpenAI account.

## Why this exists

Paperclip's first-agent wizard ("Connect a model") offers only Claude Code and
Codex. That list is a hardcoded `recommended` flag in the web UI, so a new
company created through the wizard always stops at a provider it has no account
for. Importing this package creates the company *with its CEO already
configured*, so the wizard never runs.

This is stock Paperclip. No source patch, no fork, no custom image.

## How to use it

1. In Paperclip, open the account menu at the bottom of the left sidebar →
   **Settings** → **Import**.
2. Leave the source on **GitHub repo** and paste this repository's URL.
3. Target: **Create new organization**. Type the name you want in
   **New organization name** — that name is used verbatim.
4. Review the preview, then import.

The new company arrives with a CEO on the `opencode_local` adapter, using the
server's existing OpenCode configuration. No provider key is stored in the
company, and no managed Connection is created.

## What is inside

| Path | Purpose |
|------|---------|
| `COMPANY.md` | Company name and slug (overridden by the name you type at import) |
| `.paperclip.yaml` | CEO adapter, model, runtime and permissions |
| `agents/ceo/AGENTS.md` | The stock Paperclip CEO persona |
| `skills/` | The five skills the CEO is granted, plus `agentmail` |

The CEO is configured with:

```yaml
adapter:
  type: "opencode_local"
  config:
    model: "gateway/bernie-muse-contributor"
```

`gateway` is the provider defined in the host's `opencode.json`; the model is a
gateway alias, not a provider account. Timer heartbeats are off
(`intervalSec: 0`), so an imported CEO does nothing until it is given work.

## Requirements

This package only works on a Paperclip instance whose OpenCode configuration
already defines a `gateway` provider with a `bernie-muse-contributor` model.
On any other instance the import still succeeds, but the CEO will have no
usable model until its adapter config is pointed at a model that instance has.

## Provenance

Exported from a working Paperclip 2026.916.0 company and sanitized: the
originating company name was replaced, and the org-chart image was dropped
(the GitHub import path fetches only `.md`, `skills/` and `.paperclip.yaml`).
It contains no credentials, hostnames or filesystem paths.
