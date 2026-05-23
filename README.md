# Outcall Presets for Clawie

Curated [Outcall](https://github.com/Outcall-dev/root) rule packs for common Clawie agent profiles. Drop-in egress allow-lists so operators don't have to write them from scratch.

> Outcall is owned by [`Outcall-dev`](https://github.com/Outcall-dev/root) — an independent host-level firewall project that Clawie may optionally consume. The presets here are Clawie-shaped bundles built on top of Outcall's rule format.

## Profiles (planned)

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
clawie outcall preset install coder --for-agent default-agency/coder
```

## Layout

```
outcall-presets/
├── presets/
│   ├── coder.yaml
│   ├── devops.yaml
│   ├── web-research.yaml
│   ├── marketer.yaml
│   ├── security-audit.yaml
│   └── local-only.yaml
└── tests/
```

Each preset is a versioned, signed Outcall ruleset reviewable as a PR.

## Status

Bootstrap pending. See [`clawie-dev/specs/speckit/002-container-runtime-outcall`](https://github.com/clawie-dev/specs/tree/main/speckit/002-container-runtime-outcall).

## License

MIT — see [LICENSE](LICENSE).
