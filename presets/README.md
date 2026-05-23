# Outcall presets

Curated [Outcall](https://github.com/clawie-dev/outcall) rule packs for common
Clawie agent profiles. Drop-in egress allow-lists so operators do not have to
write them from scratch. Imported per-agent via:

```bash
clawie outcall preset install <name> --for-agent <team>/<agent>
```

Each preset is a versioned, signed Outcall ruleset reviewable as a PR.

## Profiles (planned for Phase 5)

| Profile | Allows |
|---|---|
| `coder` | github.com, npmjs.org, pypi.org, crates.io, packagist.org, configured LLM provider, local CI endpoints |
| `devops` | configured cloud provider APIs, DNS providers, github.com, configured LLM provider |
| `web-research` | configured search API, configured LLM provider, arbitrary HTTP/HTTPS read-only |
| `marketer` | configured LLM provider, configured social/marketing APIs, configured analytics |
| `security-audit` | LLM provider only; no other egress |
| `local-only` | no external egress; local services only |

Each preset declares its rules, expected use, and minimum Outcall version.
