# Overnight review: Larkspur disruption-care agent

**To:** iRahulSin__larkspur-exercise  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-09-16 07:50

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Overnight, Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. agent.py is byte-identical to the shipped template, so none of the six pencil marks have been filled in.**

TONE_ADDENDUM is still 0 characters, EXTRA_TOOLS is an empty list, and LOCAL_TOOLS has no executors. run_agent(), build_tools() and tool_list() are all present but untouched from scaffold.

Run git diff against the workshop template and paste the output to confirm what, if anything, changed.

**2. search_alternatives carries a 6-character description: the literal string "search".**

Every other tool schema in build_tools() runs from 71 to 445 characters and spells out fields, required inputs and when to call it. search_alternatives gives Claude nothing to decide from, no matter which model sits behind the call.

Run python3 run.py --show-tools and paste the search_alternatives entry to confirm the description in production matches this file.

**3. No readout-trace.json exists, so no run of this agent has survived to be reviewed.**

The material states there is no committed wire run for this repository. That means nobody has seen whether the while loop in run_agent() ever hits its MAX_TOOL_CALLS of 8, or how many tool turns a real disruption case takes.

Run python3 run.py K7PQ2M --trace and commit the resulting trace.

**4. There are no eval cases in evals/cases.json, so no booking shape has been scored against this build.**

The nine tool schemas and the MAX_TOOL_CALLS=8 cap are static claims until a case exercises them. Nothing here shows whether check_policy's policy_row_id citation requirement, or confirm_rebooking's confirmation_token requirement, actually holds up across a run.

Run python3 eval_harness.py once cases exist and paste the totals.

**5. PITCH.md is unchanged from template, so no case has been made yet for what a bigger model would fix versus what the schema gaps would still break.**

The search_alternatives description problem sits in the tool layer, not the model layer. A stronger model still receives the string "search" and nothing else about when to call it or what it returns.

Run python3 bench.py --compare with a fixed tool schema against the current one before attributing any quality delta to model choice.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (226 lines)`
- `PITCH.md (unchanged template)`
- `TEAM.md (unchanged template)`

Reviewer: `claude-sonnet-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
