---
name: prompt-confusion-table-2
description: >
    Verify artifact with instructions — a prompt, skill, rule file, tool description, or agent definition
    — capturing what the model produced while working, and reporting confusion table.
    Produces a report, never an edit. Used to validate the instruction artifact.
---

# Prompt Confusion Table

The artifact is whatever text steers the model (prompt, skill, tool definition); a **site** is any
phrase, paragraph, section or rule in it — or the absence of one. This skill reports, never edits or
proposes wording. Skip it when the artifact is a few lines, or nothing of the working can be captured.

## 1. Read the traces and build the confusion table

Read every trace record in full, hunting for each and every phrase/case in the trace representing one of
the ten kinds of confusion in the **Types** list below: `confusion`, `silent-assumption`, `self-misleading`,
`stuck`, `unclear-next`, `format-unclear`, `contradiction`, `scope-unclear`, `over-specified`,
`irrelevant`.

Find as many cases as the trace actually holds — miss none, invent none. Each is found in the trace
first and traced back to its site. The types classify what you find; they are not slots to fill.

Never merge on sameness. Every moment of confusion in the trace gets its own row, however many it holds.
Do not fold two moments into one row because they share a site, a type, or a passage.

For each of the confusion record found understand where it sits, what the model was doing before and after.
**Build exactly one table, all fields required, one row per confusion case.** every moment recorded, from
every trace (passes and failures):

| # | Run | Artifact statement | Link | Type | Prompt related | Reasoning quote |
|---|---|---|---|---|---|---|
| `C<n>` | `<run id>` · `passed` / `failed` | `<the artifact's words>` at `<location>`, or `absent:` `<what would have settled it>` | `<mechanism>` | `<type>` | `true` / `false` | `<the model's words>` |

- **Run** — which trace this confusion came from, and whether it passed.
- **Artifact statement** — the artifact's (prompt/skill/...) exact words (verbatim) and where they sit;
  for an absent site, `absent:` and the statement that would have settled it.
- **Link** — how artifact words produce this confusion, in one sentence: the mechanism. Not a restatement
  of the words, and not an account of what the model did. No placeholders or stubs.
- **Type** — one of the ten kinds below.
- **Reasoning quote** — phrase/quote/part, word for word, from the model reasoning/thinking trace, that
  shows the confusion on its own.
- **Prompt related** — `true` when the confusion is about the artifact itself: what it says, or what it is
  missing and should say. `false` when the confusion is about the task and the artifact steered the model
  into it — task confusion it did not steer gets no row.

**Types** — the keywords are a reading aid, never a search as they vary model to model:

- `confusion` — says outright it does not know what is meant. `it doesn't say`, `it's unclear whether`,
  `it doesn't specify`, `ambiguous`, `this could mean`, `Hmm`, `Alternatively`, `Or maybe`
- `silent-assumption` — settles an open question without flagging that it chose. `I'll assume`,
  `presumably`, `I'll take X to mean`, `let's say`, `going with`, `I'll interpret this as`
- `self-misleading` — commits to one reading, then builds on it as settled. `as established`,
  `since we decided`, `so it must be`, `which confirms`, `building on that`
- `stuck` — nothing in the artifact can settle the matter, so it goes over the same ground again and
  again without getting any closer to an answer; or re-derives what it had already settled. `let me
  re-read`, `going back to`, `once more`, `as I said above`, `Actually`, `On second thought`,
  `Let me reconsider`
- `unclear-next` — knows the current step, not the one after it. `what should I`, `do I need to`,
  `should I also`, `then what`, `is that everything`
- `format-unclear` — knows what to say, not what shape to say it in. `what format`, `should it be a`,
  `as a list or`, `how should I present`, `in what form`
- `contradiction` — two statements collide and neither governs. `but it also says`, `that contradicts`,
  `earlier it said`, `unless`, `which conflicts with`, `Wait`, `Hold on`, `But`
- `scope-unclear` — cannot tell whether a rule applies to this case. `does this apply`,
  `is this case covered`, `only when`, `does that include`, `applies to X, but`
- `over-specified` — a stated rule does not fit the case, and is followed anyway. `the rule says`,
  `it says to`, `even though`, `doesn't fit but`, `so we must`
- `irrelevant` — clear and correct, but the model spends work on it and gets nothing. No wording marks
   it; found by a passage weighed at length that changes nothing in the output.

## 2. Write the report:

- Section 1. **What was run**. Which tests, how many of each kind, how many runs each, and who defined the suite — the
user, the user choosing from your options, you, or a corpus supplied already run.
- Section 2. **How the run itself went**. Runs started, runs that finished cleanly, and runs that failed with
error/exeption/unparseable output.
- Section 3. The confusion table. §1's single table in full, whole and unsplit.
- Section 4. Summary. Highlight important things and what was not mentioned above. No resolutions and opinions,
only facts.

Where it goes: 
No file is written without the user's agreement or provided report path. If they said where, write it there.
If they did not say, ask before writing anything, offering as an alternative that nothing is written and
the whole report comes back in the response. If they do not answer, output the report in the response and
say at the top that no files were written.
