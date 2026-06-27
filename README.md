# alfolab-market

AlfoLab's [Claude Code](https://claude.com/claude-code) plugin marketplace —
small, sharp developer plugins.

## Add the marketplace

```bash
# from GitHub
claude plugin marketplace add AlfoldiMate/alfolab-market

# …or from a local clone
claude plugin marketplace add ~/Development/alfolab-market
```

Then install a plugin:

```bash
claude plugin install cli-autocomplete@alfolab-market
claude plugin install research-this@alfolab-market
```

Or browse interactively with `/plugin`.

## Plugins

### `cli-autocomplete`

Generate and refresh rich, **git-style categorized** zsh tab-completions for any
CLI by introspecting its `--help`. Two skills:

| Skill | What it does |
|---|---|
| `/autocomplete-cli <cli>` | Introspect a CLI's `--help` (global options, subcommands, **per-subcommand** options, value enums) and write a `_<cli>` zsh completion with subcommands grouped into labelled categories that `fzf-tab` renders as sections. |
| `/autocomplete-cli-refresh <cli>` | Re-introspect a CLI whose completion already exists and update it to the current version — add new flags/subcommands, drop removed ones, refresh enums — preserving the existing category structure. |

**Highlights**
- Completes each subcommand's *own* options (e.g. `mcp add --scope`,
  `--transport`), not just the global flags.
- Value enums (`--format text|json`, `--scope local|user|project`), and
  file/dir completion for path arguments.
- git-style category groups (`[authentication]`, `[extensions & config]`, …)
  for a hand-crafted feel under `fzf-tab`.
- Works best on [commander.js](https://github.com/tj/commander.js) CLIs; the
  skill adapts the introspection for clap / cobra / click / argparse and prefers
  a CLI's native `completion zsh` generator when one exists.

Requires zsh with `compinit` (and `fzf-tab` for the grouped sections to render
as a fuzzy-filtered menu).

### `research-this`

Domain-agnostic research, from a quick orientation to a full **knowledge
collection** — cited markdown a human can read to actually understand a topic,
not just a link dump. Two skills, same source discipline at different depths:

| Skill | What it does |
|---|---|
| `/research-this <topic or question>` | Scope the question, fan out angled web searches, read primary/authoritative sources, verify load-bearing claims adversarially, then synthesize a structured collection (overview → deep-dive sections → glossary → key data → open questions → annotated sources). |
| `/overview-this <topic or question>` | The lightweight companion: a fast, grounded overview — short plain-language intro + a brief peek at one or two of the deeper/interesting parts — in one concise doc you can read in minutes. Points to `/research-this` when you want the full treatment. |

**Highlights**
- Works across **science, math, economics, politics, history, tech** — the rigor
  is fixed; the collection's shape adapts to the domain.
- Depth tiers: *brief* (one explainer), *standard* (small collection), *deep*
  (full collection with parallel per-subtopic research).
- Sources are non-negotiable: real URLs, primary-where-possible, cited inline,
  with contested/uncertain claims flagged — no fabricated references.
- Writes to `~/Knowledge/research/<slug>/` by default, built to be read top-to-bottom.

## License

[MIT](./LICENSE)
