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

## License

[MIT](./LICENSE)
