---
name: autocomplete-cli
description: Generate a rich, git-style categorized zsh tab-completion for a CLI by introspecting its --help. Use when the user wants shell completion for a command-line tool (e.g. "make zsh completion for foo", "autocomplete for the bar cli").
argument-hint: "[cli-name]"
allowed-tools: Bash, Read, Write, Edit
---

# Autocomplete a CLI

Generate a high-quality zsh completion function (`_<cli>`) for the CLI named in
the user's argument. The result should feel hand-crafted: global options with
value enums, **per-subcommand** options (not just globals), and subcommands
grouped into **git-style labelled categories** that `fzf-tab` renders as
sections.

The target CLI is the first argument (e.g. `/autocomplete-cli kubectl` →
generate for `kubectl`). If the user gave no CLI name, ask which command to
complete.

## Read the methodology first

Before doing anything, read the full generation reference:

`${CLAUDE_PLUGIN_ROOT}/skills/autocomplete-cli/reference.md`

It contains the exact introspection technique (incl. the commander.js
local-option diff), the `_arguments`/`_describe` spec syntax, the categorized
grouping pattern, fpath/compinit activation, and a zpty verification harness.
Follow it.

## Procedure (summary — the reference has the details)

1. **Verify** the CLI exists: `which <cli>` and capture `<cli> --version`. If it
   isn't installed, stop and tell the user.
2. **Check for a native generator** before hand-rolling: try
   `<cli> completion zsh` / `<cli> completions zsh` / `<cli> --help | grep -i complet`.
   Many clap/cobra/click tools ship one. If a good native generator exists,
   offer it — but still hand-roll when the user wants the categorized-group UX
   this skill specializes in.
3. **Pick the fpath dir** (reference §0): prefer an existing writable dir on
   `$fpath` (commonly `~/.zfunc`); else create `~/.zfunc` and make sure the rc
   file adds it before `compinit`.
4. **Introspect** (reference §1): parse global options + commands from
   `<cli> --help`; for each subcommand run `<cli> <sub> --help` and extract its
   *local* options (diff against globals for commander.js; scrape directly for
   clap/cobra/click). Recurse one level for nested command groups. Detect value
   enums (`choices:`, scope/transport-style prose), and path args.
5. **Design categories** (reference §3): group subcommands by user intent into
   2–6 labelled buckets at each level. This is the part that makes it feel
   bespoke — think about it, don't sort alphabetically.
6. **Write** `<fpath-dir>/_<cli>`: `#compdef <cli>` first line; global options at
   top level; one handler function per command group offering local options +
   `--help`; multiple `_describe -t <tag> '<header>' <array>` calls for the
   grouped categories; value enums and `_files`/`_files -/` actions where
   appropriate.
7. **Activate**: `zsh -n <file>` (must pass) then `rm -f ~/.zcompdump*`. Tell the
   user to open a new terminal or run `exec zsh`.
8. **Verify** with the zpty harness (reference §5): confirm `<cli> <TAB>` shows
   the grouped headers, `<cli> <sub> --<TAB>` shows that subcommand's options,
   and at least one value enum (e.g. a `--scope`/`--format`) completes. Report
   what you verified.

## Notes
- Match the user's existing completion style if they already have `_<cli>` or
  other custom completions — reuse their fpath dir and zstyle conventions.
- The completion is **static**: it's a snapshot of the CLI's current surface.
  When the CLI updates, run `/autocomplete-cli-refresh <cli>` to regenerate.
- Keep the file readable and commented so it can be maintained by hand later.
