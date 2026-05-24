# Outcall Presets for Clawie

Curated [Outcall](https://github.com/outcall-dev/root) rule packs for common
Clawie agent profiles. Drop-in egress allow-lists so operators don't have to
write them from scratch.

> Outcall is owned by [`outcall-dev`](https://github.com/outcall-dev/root) — an
> independent host-level firewall project that Clawie may optionally consume.
> The presets here are Clawie-shaped bundles built on top of Outcall's rule
> format.

## Shipped presets

| Preset | Allows | Intent identity |
|---|---|---|
| [`clawie-default`](presets/clawie-default.yaml) | Anthropic Messages API + OpenAI Chat Completions API | `agent.name == "clawie-chat"` |

## Roadmap

These are the profiles we want to ship next; PRs welcome.

| Profile | Allows |
|---|---|
| `coder` | github.com, npmjs.org, pypi.org, crates.io, packagist.org, configured LLM provider, local CI endpoints |
| `devops` | configured cloud provider APIs (AWS/GCP/Azure/Fly/CF), DNS providers, github.com, configured LLM provider |
| `web-research` | configured search API, configured LLM provider, arbitrary HTTP/HTTPS (read-only) |
| `marketer` | configured LLM provider, configured social/marketing APIs, configured analytics |
| `security-audit` | LLM provider only; no other egress (offline analysis) |
| `local-only` | no external egress; local services only |

## Install

```bash
# Manual: drop into the Outcall rules directory and reload
sudo cp presets/clawie-default.yaml /etc/outcall/rules.d/
sudo outcall rules reload

# Via Clawie (per-team)
node ace outcall:sync --team <team-slug>
node ace outcall:sync --team <team-slug> --hosts api.anthropic.com,api.openai.com,api.github.com
```

The `node ace outcall:sync` command in Clawie writes
`/etc/outcall/rules.d/clawie-team-<slug>.yaml` for the named team and
asks the daemon to reload. By default the team's chat intent is allowed
to reach `api.anthropic.com` and `api.openai.com`; pass `--hosts` with a
comma-separated list to override. The team slug must already exist
(`teams:create` first). Preferred over manual install when you have
multiple teams — each team gets its own rule file, scoped by
`agent.name == "clawie-<team-slug>-chat"`.

## Layout

```
outcall-presets/
├── presets/
│   └── clawie-default.yaml    ← currently the only published preset
└── README.md
```

Each preset is a versioned Outcall ruleset reviewable as a PR.

## Status

Bootstrapped. `clawie-default` is the production preset used by Clawie's
`chat` intent. The other six profiles are planned. See
[spec 002](https://github.com/clawie-dev/specs/tree/main/speckit/002-container-runtime-outcall)
for the design contract these presets implement.

## License

MIT — see [LICENSE](LICENSE).
