# research-this — methodology reference

This is the full playbook the `research-this` skill follows. It is
domain-agnostic: the same rigor applies to a physics question, a math proof, a
macro-economics debate, a piece of legislation, or a historical episode. What
changes per domain is the *collection shape* (§4) and the *kinds of sources*
that count as authoritative (§2). The deliverable is always a **knowledge
collection**: documents a human can read to actually understand the topic.

---

## §0. The job

Produce, from a topic or question, a self-contained reading collection that
takes a motivated non-specialist from zero to real understanding:

- the **core concepts** and vocabulary, defined as introduced;
- the **mechanism / argument / chain of reasoning** — the *why*, not just the *what*;
- the **evidence**, with figures, dates, and primary sources;
- the **disagreements and open questions**, honestly represented;
- **where to go next** — the best sources, ranked.

Coverage without comprehension is failure. A pile of links is not a collection.

---

## §1. Depth tiers — pick one up front, state it

| Tier | When | Research effort | Deliverable |
|---|---|---|---|
| **Brief** | Narrow, factual, or "just explain X quickly" | A handful of inline searches; read 3–6 sources | One markdown doc (`<slug>.md`): explainer + sources |
| **Standard** | A real topic the reader wants to understand | 3–6 sub-questions; read 10–20 sources | A small collection: `README` + 3–5 section docs + sources |
| **Deep** | Big, contested, or technical; "understand it properly" | Parallel research per sub-question; read 20–40+ sources; adversarial verification | Full collection: index, overview, per-subtopic deep-dives, glossary, key data, open questions, annotated sources |

Default to **standard** unless the topic or the user signals otherwise. Words
like "deep," "properly," "comprehensive," "thesis," "everything about" → deep.
"quick," "tl;dr," "just tell me" → brief.

Scale honestly: don't inflate a quick question into a thesis, or compress a deep
topic into a paragraph. For **deep** tiers the rich collection is the *headline
deliverable* — it must stand on its own.

---

## §2. Source strategy — fan out, then go primary

**Fan out.** For each sub-question, run several *angled* searches, not one. Vary
the framing so different sources surface:

- plain question ("how does X work")
- technical/term-of-art framing (the field's actual vocabulary)
- the *opposing* or critical framing ("X criticism", "X problems", "X debunked")
- temporal ("X 2025", "latest X research", "history of X")
- authoritative-source framing ("X review article", "X primary source", site/org names)

**Source quality tiers** (prefer higher; triangulate across tiers):

1. **Primary / authoritative** — peer-reviewed papers, official statistics,
   standards bodies, court rulings, legislation text, datasets, original
   announcements, textbooks, the actual people/orgs involved.
2. **High-quality secondary** — review articles, reputable encyclopedias,
   established outlets with editorial standards, expert explainers, institutional
   reports.
3. **Tertiary / informal** — blogs, forums, Q&A sites, news aggregation. Useful
   for orientation and leads; **verify before relying on**.

Domain notes:
- **Science / medicine** — prefer peer-reviewed + reviews/meta-analyses; note
  study design, sample size, replication, consensus vs. preliminary.
- **Math / CS theory** — prefer textbooks, lecture notes, original papers;
  reproduce definitions and key proof *ideas* precisely.
- **Economics / finance** — separate theory, empirical evidence, and policy
  opinion; cite data sources (central banks, statistical agencies) directly.
- **Politics / policy / law** — read the primary text (bill, ruling, treaty);
  represent multiple partisan perspectives fairly; attribute opinions to who
  holds them; date everything.
- **History** — prefer primary documents and academic historians;
  note historiographical debate and how interpretation has shifted.

**Record every source as you go**: title, author/org, date, URL, and a one-line
note on what it supports and its tier. This becomes the sources doc.

---

## §3. Verification — adversarial, not credulous

For any claim that is **load-bearing, surprising, contested, or quantitative**:

- find a **second independent** source that confirms it, **or**
- find a source that **disputes** it — then represent the disagreement.

Rules:
- Distinguish **established fact** / **mainstream interpretation** / **fringe or
  contested** / **open question** — and label which in the writing.
- A single source ≠ verified. Coincidence of sources that all cite the *same*
  origin ≠ independent confirmation — trace claims to their root.
- Numbers, dates, quotes, and attributions get checked against the primary
  source. **Never paraphrase a statistic from memory.**
- If you cannot verify something that matters, say so explicitly ("reported by
  X but not independently confirmed").
- **No fabrication, ever** — not a URL, not a quote, not an author, not a
  figure. A missing source is a gap to flag, never a thing to invent.

For deep tiers, run a short **completeness/skeptic pass** at the end: what's
missing, what claim is thinly sourced, what counter-argument went unaddressed,
what's the strongest case *against* the synthesis? Fix what that surfaces.

---

## §4. Collection shape — adapt to the domain

The outline *is* the collection structure. Decompose the topic into
sub-questions, then map them onto a shape. Templates (adapt, don't follow
blindly):

**Explainer / "how does X work" (science, tech, mechanisms)**
`overview → fundamentals/prerequisites → the mechanism step by step →
variants & edge cases → applications/implications → limits & open questions →
glossary → sources`

**Concept / theorem (math, CS theory)**
`statement in plain words → why it matters → prerequisites & definitions →
intuition → the argument/proof sketch → worked example → consequences &
related results → sources`

**Event / episode (history, current affairs)**
`what happened (summary) → background & causes → timeline → key actors →
consequences & aftermath → interpretations/debates → sources`

**Debate / contested question (economics, policy, politics)**
`the question → why it's contested → position A (best case + evidence) →
position B (best case + evidence) → what the evidence actually shows →
points of consensus → open questions → sources`

**Decision / comparison ("X vs Y", "should I/we…")**
`the decision & criteria → options → comparison across criteria (table) →
trade-offs → recommendation w/ caveats → sources`

**Survey / landscape ("state of X")**
`overview → taxonomy/map of the field → major threads (one section each) →
key players/works → trajectory & open problems → sources`

Every collection includes, regardless of shape:
- **An index/overview** the reader starts from (what's here, in what order).
- **A glossary** when the topic has real jargon.
- **A sources list** with full, real citations.
- **Open questions / what's uncertain** — never omit this.

---

## §5. Writing the collection — make it understandable

File layout (standard/deep):

```
~/Knowledge/research/<slug>/
  README.md            # index + 1-paragraph TL;DR + how to read this + reading order
  00-overview.md       # the executive understanding: the whole story in ~1–2 pages
  01-<subtopic>.md     # deep-dive sections (one per sub-question)
  02-<subtopic>.md
  ...
  glossary.md          # key terms, plain-language definitions
  data.md              # key figures, tables, datasets (where relevant)
  open-questions.md    # what's unsettled, contested, or unknown
  sources.md           # annotated, tiered citation list
```

(Brief tier: collapse all of this into one `<slug>.md` with sections.)

Writing rules:
- **Build from fundamentals up.** Don't assume the vocabulary; define terms on
  first use and link to the glossary.
- **Explain the *why* and the mechanism**, not just conclusions. Give intuition
  before formalism. Use analogies, then make them precise.
- **Show the evidence.** Concrete figures, dates, examples, worked cases. Tables
  for comparisons and data.
- **Cite inline.** Every non-obvious claim gets a marker, e.g. `[S3]`, tied to
  `sources.md`. Mark contested claims (`[contested]`) and uncertain ones
  (`[uncertain]`).
- **Represent disagreement fairly.** Give each serious position its strongest
  form before any critique. Attribute opinions to who holds them.
- **Write for an intelligent non-specialist** unless the user specified a level.
  Plain language; jargon earned, not assumed.
- **End each deep-dive** with "what's still unclear here" where applicable.

---

## §6. Parallel research (deep tier)

For deep topics, dispatch the sub-questions to parallel `Agent` researchers so
gathering happens concurrently. Pattern:

- Give each agent **one sub-question**, the search strategy (§2), the source
  tiers, and the verification rules (§3).
- Ask each to return **structured notes**: findings, each tied to a source with
  URL + tier, plus explicit "confidence" and "disagreements found."
- You (the orchestrator) then **verify across** the returned notes, dedupe
  sources, resolve contradictions between agents, run the skeptic pass (§3), and
  write the synthesis yourself — agents gather, you synthesize.

Keep the agent count proportional to the topic (a handful for most deep topics).
Don't fan out a brief/standard topic — inline search is faster there.

---

## §7. Final checklist before delivering

- [ ] Depth tier chosen and matched by the actual output.
- [ ] Every section answers a real sub-question; outline → collection structure.
- [ ] Mechanisms / arguments explained, not just stated. A reader would *get it*.
- [ ] Jargon defined; glossary present if needed.
- [ ] Load-bearing claims verified or flagged; contested points represented fairly.
- [ ] Every non-obvious claim cited inline; `sources.md` complete with real URLs.
- [ ] Open-questions / uncertainty section present.
- [ ] No fabricated sources, quotes, or figures.
- [ ] Output path(s) printed; one-line confidence + gaps note given to the user.
