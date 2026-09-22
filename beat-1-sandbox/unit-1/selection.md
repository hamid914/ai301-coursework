# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68

**Verdict output**

issue-select: grade these candidate first issues: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/8 https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69 https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68

● Skill(issue-select)
Successfully loaded skill

  Read 3 files

I'll gather evidence from the live repo for each of the three issues.

  Ran 15 shell commands

I have enough evidence to grade all three. Applying the rubric.

Grading summary

Repo facts (measured against today, 2026-09-21):
- Last default-branch commit: 2026-09-16 (5 days ago), authored by Aburke225 — the sole committer and the author of all three issues.
- Last push to any branch: 2026-09-16.
- docs/CONTRIBUTING.md exists; contains no ban on AI-generated contributions (silence passes).
- No closed PRs; only 1 open PR, targeting issue #60 (not any of these three).

---
Issue #8 — "Review generator never combines feedback across a user's projects"

- Maintainer alive: pass — last default-branch commit 2026-09-16 (<90d).
- Repo in use: pass — pushed 2026-09-16 (<6mo).
- AI policy: pass — docs/CONTRIBUTING.md is silent on AI use.
- Claimed: pass — no assignee, no linked PRs, no comments at all.
- Scope: pass — bug is bounded, two specific files named, no umbrella/tracking, no design debate. (Labeled tier-3/Advanced with 7–10h effort — the rubric doesn't gate on difficulty, so this still passes.)
- Verdict: accept.

Issue #69 — "Output parser crashes on a top-level JSON array fallback"

- Maintainer alive: pass — same last-commit signal.
- Repo in use: pass.
- AI policy: pass.
- Claimed: pass — no assignee, no linked PRs. jacho15 posted claim + repro (2026-09-19) but per the Path Review house rule, another student's claim comment does not block.
- Scope: pass — labeled good first issue / tier-1, precise bug with named files, xfail marker removal spelled out. Not umbrella, not debated.
- Verdict: accept.

Issue #68 — "Keyword search raises ZeroDivisionError when the index is empty"

- Maintainer alive: pass.
- Repo in use: pass.
- AI policy: pass.
- Claimed: pass — no assignee, no linked PRs. yulijasso posted claim + reproduction + fix plan (2026-09-20) but house rule ignores classmate claims.
- Scope: pass — good first issue / tier-1, isolated one-line guard, files and xfail marker specified.
- Verdict: accept.

---
Ranked read-out (fit to profile)

All three accepted. Fit ordering for a Python/RAG-fluent PhD student:

1. #68 — Tier-1 bug in the BM25 retriever; empty-corpus guard is a minimal, low-risk change that lands in the retrieval half of the RAG stack the user already knows (FAISS/RAG on the profile). Tightest scope of the three.
2. #69 — Tier-1 bug, similar size, in the LLM output parser; straightforward dict vs list fallback, plain Python + pytest work — a clean fit but slightly further from the user's retrieval strengths than #68.
3. #8 — Tier-3, 7–10h, design-heavier refactor of _consolidate_feedback plus prompt-template changes. Best alignment with the user's LangChain/RAG design experience, but heaviest lift for a first contribution.

```
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "Maintainer contribution in issues", "grade": "pass", "evidence": "Last default-branch commit by Aburke225 on 2026-09-16 (5 days before capture)."},
      {"name": "Latest release date", "grade": "pass", "evidence": "Repo pushedAt 2026-09-16, well within 6 months."},
      {"name": "Fully AI usage is not allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI ban; policy is silent on AI use."},
      {"name": "Claimed check", "grade": "pass", "evidence": "assignees: []; no linked PRs; only claim comment is from yulijasso (author_association NONE) — ignored under Path Review house rule."},
      {"name": "Scope check", "grade": "pass", "evidence": "Labels include 'good first issue' and 'tier-1'; body names one file, one guard, and the specific xfail marker to remove."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69",
    "checks": [
      {"name": "Maintainer contribution in issues", "grade": "pass", "evidence": "Last default-branch commit by Aburke225 on 2026-09-16 (5 days before capture)."},
      {"name": "Latest release date", "grade": "pass", "evidence": "Repo pushedAt 2026-09-16, well within 6 months."},
      {"name": "Fully AI usage is not allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI ban; policy is silent on AI use."},
      {"name": "Claimed check", "grade": "pass", "evidence": "assignees: []; no linked PRs; only claim comment is from jacho15 (author_association NONE) — ignored under Path Review house rule."},
      {"name": "Scope check", "grade": "pass", "evidence": "Labels 'good first issue' / 'tier-1'; body pinpoints AttributeError in output_parser.py fallback plus the xfail marker to drop."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/8",
    "checks": [
      {"name": "Maintainer contribution in issues", "grade": "pass", "evidence": "Last default-branch commit by Aburke225 on 2026-09-16 (5 days before capture); Aburke225 renamed this issue on 2026-09-16."},
      {"name": "Latest release date", "grade": "pass", "evidence": "Repo pushedAt 2026-09-16, well within 6 months."},
      {"name": "Fully AI usage is not allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI ban; policy is silent on AI use."},
      {"name": "Claimed check", "grade": "pass", "evidence": "assignees: []; no linked PRs; comments: []."},
      {"name": "Scope check", "grade": "pass", "evidence": "Body names two files (review_generator.py, prompt_templates.py) and a specific defect in _consolidate_feedback; not an umbrella or tracking issue and no design debate in-thread. (Labeled tier-3 / 7–10h — difficulty is not a rubric gate.)"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

agreement: 7/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)
agreement: 16/20 scored items  (bar: 18/20: below the bar)
agreement: 18/20 scored items  (bar: 18/20: PASS)
agreement: 19/20 scored items  (bar: 18/20: PASS)

**Issue analysis**

`issue-04`. The gold label is `accept`. My rubric's decision was `reject`. The reasoning that produced my result was driven by the Scope check. The issue body requests rule previews and ends the list with "etc." Because my Scope check requires a "well-defined, bounded piece of work with a settled specification," the skill interpreted "etc." as an unsettled, open-ended specification that lacked a firm boundary, causing it to fail the issue.

**Check rationale**

"The issue describes a well-defined, bounded piece of work with a settled specification. It is not an open-ended feature wish, tracking list, or umbrella issue. The design is not actively being debated, and it does not have a history of several abandoned (closed, unmerged) PRs. (Note: Checklists, multiple causes, or suggested fixes for a single bug are acceptable)"

The reasoning behind its current form is to catch massive tracking lists and heavily debated design wishes without accidentally punishing well-structured bug reports. Earlier iterations falsely rejected issues like `issue-19` just because they contained numbered lists of bug causes. I also specified *several* abandoned PRs to avoid throwing out perfectly good issues that just happened to have a single stale PR from a previous contributor.

**Trade-offs**

By requiring a "settled specification," this Scope check gives up otherwise easy, valid issues that are written casually. As seen with `issue-04`, if a maintainer uses shorthand like "etc." instead of enumerating every single acceptance criterion, the rubric interprets it as an unbounded umbrella task and rejects it, missing out on what is actually a simple "good first issue."

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Issue #68 is a great fit for my time and interests. It is a minimal, low-risk fix (a Tier-1 bug) located in the BM25 retriever, which directly aligns with my daily Python backend work and familiarity with retrieval systems and RAG architectures.
2. The verdict correctly identified that the repository is highly active (a commit within the last 5 days) and that the contribution policy allows AI usage. However, the rubric could not weigh the technical domain of the issue; it doesn't know that I specifically have experience with search indexes and retrieval logic, making this a much faster task for me than a frontend UI issue.
3. I anticipate zero difficulty claiming it. Even though another contributor (`yulijasso`) posted a claim comment recently, the Path Review house rules explicitly state that classmate claims do not block an issue, so I am free to proceed.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
