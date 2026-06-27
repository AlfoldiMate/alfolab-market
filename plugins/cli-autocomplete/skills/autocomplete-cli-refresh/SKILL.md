---
name: autocomplete-cli-refresh
description: Re-introspect a CLI and update its existing zsh completion to match the current installed version — add new flags/subcommands, drop removed ones, refresh value enums. Use after upgrading a CLI, or when its completion feels stale or wrong.
argument-hint: "[cli-name]"
allowed-tools: Bash, Read, Write, Edit
---

# Refresh a CLI's completion

The CLI named in the argument already has a generated zsh completion (`_<cli>`);
the CLI has since changed (new version, new subcommands/flags) and the
completion should be brought back in sync. Regenerate it, show what changed, and
preserve the hand-tuned bits (especially the category grouping).

The target CLI is the first argument (e.g. `/autocomplete-cli-refresh claude`).
If none is given, list the `_*` files on the user's `$fpath` and ask which to
refresh.

## Read the methodology first

This skill shares the same generation methodology as `autocomplete-cli`. Read:

`${CLAUDE_PLUGIN_ROOT}/skills/autocomplete-cli/reference.md`

## Procedure

1. **Locate the existing completion.** Search `$fpath` dirs for `_<cli>`
   (`zsh -ic 'print -l $fpath'` then look for the file). If none exists, this is
   a fresh generation — defer to `/autocomplete-cli <cli>` instead and say so.
2. **Capture the current state.** Read the existing `_<cli>` file. Note its
   fpath dir, its category groupings (the `_describe -t <tag> '<header>'`
   blocks), any custom value helpers, and any hand edits worth keeping. Record
   the CLI version the file was built for if noted in a comment.
3. **Re-introspect** the now-installed CLI exactly as in the reference (§1):
   global options, subcommands, per-subcommand local options, value enums,
   nested groups.
4. **Diff old vs new** and surface it to the user before writing:
   - **added** subcommands / options / value choices,
   - **removed** ones,
   - **changed** arg types or enums.
   A concise bullet list is enough.
5. **Regenerate**, preserving intent:
   - Keep the existing **category structure** and headers; slot new subcommands
     into the most fitting existing group, and only add a new group if a genuinely
     new area of the CLI appeared. Remove groups that became empty.
   - Keep custom value helpers and any deliberate hand edits unless the CLI
     change makes them wrong.
   - Update the version-stamp comment at the top if present (or add one).
6. **Write** the updated `_<cli>` back to the same fpath dir.
7. **Activate**: `zsh -n <file>` (must pass) then `rm -f ~/.zcompdump*`. Tell the
   user to `exec zsh` / open a new terminal. (Editing an existing file is picked
   up on next completion even without this, but clearing the dump is safe.)
8. **Verify** the changed areas with the zpty harness (reference §5): at minimum
   probe a newly-added subcommand/flag and one existing grouped list to confirm
   nothing regressed. Report the diff you applied and what you verified.

## Notes
- Be conservative: a refresh should read as a *diff*, not a rewrite. Don't
  re-flow the whole file or re-bikeshed categories that already work.
- If the CLI gained a native `completion zsh` generator since the last run,
  mention it — the user may prefer to switch.
