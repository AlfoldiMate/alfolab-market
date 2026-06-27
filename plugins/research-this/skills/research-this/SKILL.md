---
name: research-this
description: Research any topic in depth — scientific, mathematical, economic, political, historical, technical — and produce a cited knowledge collection that brings a human reader from zero to genuine understanding. Use when the user wants a researched explainer, literature scan, briefing, or "explain/understand X properly" with sources.
argument-hint: "[topic or question]"
allowed-tools: WebSearch, WebFetch, Read, Write, Edit, Bash, Agent
---

# Research This

Research the topic given in the argument and deliver a **knowledge collection**:
a set of markdown documents, scaled to the topic's depth, that a motivated human
reader can read top-to-bottom and come away genuinely understanding the subject —
not just a summary, but the concepts, the evidence, the disagreements, and where
to go next, all grounded in real cited sources.

The topic is the argument (e.g. `/research-this how do mRNA vaccines work`,
`/research-this the 2008 financial crisis`, `/research-this P vs NP`). The skill
is **domain-agnostic** — the same procedure serves a science, math, economics,
politics, history, or engineering question. The *shape* of the collection adapts
to the domain (see the reference); the *rigor* does not.

## Read the methodology first

Before researching, read the full methodology:

`${CLAUDE_PLUGIN_ROOT}/skills/research-this/reference.md`

It covers scoping, the fan-out search strategy, source quality tiers,
adversarial verification of claims, the domain-adaptive collection structures,
the citation discipline, and the depth/effort ladder. Follow it.

## Procedure (summary — the reference has the details)

1. **Scope.** Restate the topic as a sharp research question. If it is genuinely
   underspecified in a way that changes the research (audience level, region,
   time period, which sub-question), ask **2–3** clarifying questions first.
   Otherwise pick sensible defaults, state them, and proceed — don't stall.
2. **Pick depth.** Choose a tier (reference §1): *brief* (quick explainer, ~1
   doc), *standard* (multi-section collection), or *deep* (full collection with
   per-subtopic deep-dives). Deep topics **require** a collection rich enough to
   stand on its own — that is the headline deliverable.
3. **Plan the outline.** Decompose into sub-questions / sections appropriate to
   the domain (reference §4 has templates per domain). This outline becomes the
   collection's structure.
4. **Fan out research.** For each sub-question run multiple angled searches
   (reference §2). For deep tiers, dispatch parallel `Agent` researchers — one
   per sub-question — to gather in parallel; for brief/standard do it inline.
   Prefer primary & authoritative sources; record every source with a URL.
5. **Read sources, don't skim titles.** `WebFetch` the promising ones and pull
   actual facts, figures, quotes, dates, and the *reasoning*. Capture
   disagreements between sources, not just consensus.
6. **Verify claims adversarially** (reference §3). For load-bearing or surprising
   claims, find a second independent source or a source that disputes it. Flag
   what is contested, uncertain, or thinly sourced. Never launder a guess as a
   fact.
7. **Synthesize the collection.** Write the docs (reference §5 for layout):
   an index/overview, the deep-dive sections, a glossary of key terms, a
   key-figures/data section where relevant, open questions, and a sources list
   with full citations. Explain mechanisms and *why*, define jargon on first use,
   build from fundamentals up. Write for an intelligent non-specialist unless
   told otherwise.
8. **Cite inline.** Every non-obvious claim carries a source marker tying back to
   the sources list. Distinguish established fact from interpretation from open
   question.
9. **Deliver.** Default output: a folder under `~/Knowledge/research/<slug>/`
   (markdown collection). Confirm or adjust the location/format with the user if
   they indicated a preference. Tell them what was written and the confidence /
   gaps.

## Output location

Default to `~/Knowledge/research/<topic-slug>/` (the user keeps reference
material under `~/Knowledge/`). For a *brief* tier, a single
`~/Knowledge/research/<slug>.md` is fine. Always print the path(s) written and a
one-line confidence + open-gaps note.

## Principles

- **Understanding over coverage.** The test is whether a reader *gets it*
  afterward — mechanisms, intuition, and the "why," not a link dump.
- **Sources are non-negotiable.** Real URLs, primary where possible, cited
  inline. No fabricated references or quotes — ever.
- **Honest uncertainty.** Mark contested/uncertain/thin claims as such. Saying
  "the evidence is mixed" is a finding, not a failure.
- **Right-sized.** Match length and parallelism to the depth tier; don't turn a
  quick question into a thesis or a deep topic into a paragraph.
