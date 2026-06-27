---
name: overview-this
description: Give a fast, well-grounded overview of any topic — a short plain-language introduction plus a brief peek at one or two of the deeper/interesting parts — so the reader gets oriented quickly and knows whether to dig further. Use when the user wants a quick "what is X / give me the gist" with a taste of depth, not a full research collection. The deep counterpart is /research-this.
argument-hint: "[topic or question]"
allowed-tools: WebSearch, WebFetch, Read, Write, Edit
---

# Overview This

Give a **fast, grounded overview** of the topic in the argument: a short
plain-language introduction that gets a reader oriented, plus a brief look at one
or two of the topic's **deeper or most interesting parts** — enough to convey
that there's real substance underneath, without writing a full report.

This is the lightweight companion to `/research-this`. Where `research-this`
produces a multi-doc knowledge collection, `overview-this` produces **one
concise overview** the reader can absorb in a few minutes. Same honesty about
sources and uncertainty; far smaller scope.

The topic is the argument (e.g. `/overview-this what is CRISPR`,
`/overview-this the Suez Canal`, `/overview-this zero-knowledge proofs`). Works
across any domain — science, math, economics, politics, history, tech.

## Shared methodology

For source quality tiers, the fan-out search pattern, and the
no-fabrication / verification discipline, the canonical reference is the sibling
skill's playbook:

`${CLAUDE_PLUGIN_ROOT}/skills/research-this/reference.md`

You don't need the full depth machinery here — just §2 (sources) and §3
(verification). Apply them at a light touch: a few good sources, claims checked
enough not to mislead.

## Procedure

1. **Read the question.** Restate the topic in one sharp line. Don't ask
   clarifying questions unless it's truly ambiguous — overview is meant to be
   quick; pick a sensible reading and state any assumption in one phrase.
2. **Quick grounding pass.** Run a small handful of angled searches (reference
   §2) and read 3–6 solid sources — prefer authoritative/primary, but keep it
   light. Pull the real facts, figures, and the *why*; note anything genuinely
   contested.
3. **Identify the substance.** Decide what the 3–5 core ideas are, and pick the
   **one or two deepest/most interesting facets** worth a short peek (a
   surprising mechanism, a key debate, a hard sub-problem, a pivotal event).
4. **Write the overview** (structure below). Short, plain language, builds from
   nothing. Cite the load-bearing claims.
5. **Deliver.** Show the overview in the response. If it's substantial or the
   user wants to keep it, also offer/write
   `~/Knowledge/research/<slug>-overview.md`. End with a one-line pointer:
   "run `/research-this <topic>` for the full cited collection."

## Overview structure

Keep it to roughly **one screen / ~½–1 page**:

1. **TL;DR** — 2–4 sentences. If the reader stops here, what should they know?
2. **What it is & why it matters** — a short, plain-language introduction; define
   the essential terms inline.
3. **The core ideas** — 3–5 tight bullets covering the shape of the topic.
4. **A deeper peek** — 1–2 short paragraphs going *one level down* on the most
   interesting/important facet(s): the actual mechanism, the live debate, or the
   hard part. This is what distinguishes an overview from a dictionary entry —
   show that there's depth, briefly.
5. **Where it's unsettled** — one line on what's contested or unknown (if
   anything). Don't skip honest uncertainty.
6. **Go deeper** — 2–4 of the best sources (real URLs), plus the
   `/research-this` pointer.

## Principles

- **Fast but not shallow.** Orientation first, then a real taste of depth — not
  a list of links, not a glossary entry.
- **Grounded.** Real sources, cited for the load-bearing claims; no fabricated
  facts, quotes, or URLs. If unsure, say so briefly.
- **Right-sized.** One concise doc/answer. If the topic clearly needs more,
  point to `/research-this` rather than quietly expanding into a full report.
