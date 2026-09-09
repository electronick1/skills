---
name: prompt-confusion-table
description: >
    Verify an instruction artifact — a prompt, skill, rule file, tool description, or agent definition
    — capturing what the model produced while working, and reporting findings.
    Produces a report, never an edit. Used to validate the instruction artifact.
---

# Prompt Confusion Table

**Understand how the run went, build confusion table, and prepare detailed report **

The artifact is whatever text steers the model (prompt, skill, tool definition); a **site** is any
phrase, paragraph, section or rule in it — or the absence of one. This skill reports, never edits or
proposes wording. Skip it when the artifact is a few lines, or nothing of the working can be captured.

## 1. Read the traces and build the confusion table

Read every trace in full, hunting for each and every phrase/case in the trace representing one of the ten
kinds of confusion in the **Types** list below: `confusion`, `silent-assumption`, `self-misleading`,
`stuck`, `unclear-next`, `format-unclear`, `contradiction`, `scope-unclear`, `over-specified`,
`irrelevant`.

You must extract each and every phrase/case for every type, no exceptions.

For each of the confusion record found understand where it sits, what the model was doing before and after,
and whether the final output differed. **Build exactly one table, all fields required, one row per confusion
case.** every moment recorded, from every trace (passes and failures):

| # | Run | Artifact statement | Link | Type | Prompt related | Reasoning quote | Then did | Output |
|---|---|---|---|---|---|---|---|---|
| `C<n>` | `<run id>` · `passed` / `failed` | `<the artifact's words>` at `<location>`, or `absent:` `<what would have settled it>` | `<mechanism>` | `<type>` | `true` / `false` | `<the model's words>` | `<verb>` | `<differed, and how>` / `same` |

- **Run** — which trace this confusion came from, and whether it passed.
- **Artifact statement** — the artifact's (prompt/skill/...) exact words (verbatim) and where they sit;
  for an absent site, `absent:` and the statement that would have settled it.
- **Link** — how these words produce this confusion, in one sentence: the mechanism. Not a restatement
  of the words, and not an account of what the model did.
- **Reasoning quote** — phrase/quote/part, word for word, that represents such confusion in model
  reasoning/thinking trace.
- **Then did** — one of `chose` · `skipped` · `repeated` · `invented` · `changed`. What it did, not what
  it said. **Output** — `differed`, and how, or `same`.
- **Prompt related** — `true` when the confusion is about the artifact: what it says, or what it missing
  and should says. `false` when it is about the task the model was given (problem solving process not
  related to the artifact/prompt/skill).

**Types** — one per row. The keywords are a reading aid, never a search as they vary model to model:

- `confusion` — says outright it does not know what is meant. `it doesn't say`, `it's unclear whether`,
  `it doesn't specify`, `ambiguous`, `this could mean`, `Hmm`, `Alternatively`, `Or maybe`
- `silent-assumption` — settles an open question without flagging that it chose. `I'll assume`,
  `presumably`, `I'll take X to mean`, `let's say`, `going with`, `I'll interpret this as`
- `self-misleading` — commits to one reading, then builds on it as settled. `as established`,
  `since we decided`, `so it must be`, `which confirms`, `building on that`
- `stuck` — loops, or re-derives something already settled. `let me re-read`, `going back to`,
  `once more`, `as I said above`, `Actually`, `On second thought`, `Let me reconsider`, or a passage
   repeated almost word for word
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
