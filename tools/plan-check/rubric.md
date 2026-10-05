# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis Grounding | The plan's diagnosis read against the repro-evidence block | The diagnosis explicitly explains the behavior shown in the reproduction evidence without contradicting or ignoring it. | required |
| Bounded Scope | The plan's scope section | It explicitly names the specific files it will change AND clearly states what it will not touch to prevent scope creep. | required |
| Executability | The plan's approach and file list | The approach is concrete enough that a stranger could start building it immediately (not just a promise to "investigate" or "poke around"). | required |
| Decisive Test Plan | The plan's test section read against the repro-evidence block | It states an observable expected outcome (e.g., expected terminal output) rather than a vague "run the test suite" or "see if it works". | required |
| Thread and Convention | The draft plan comment read against thread highlights and repo facts | The comment engages with any explicit maintainer direction in the thread, promises only what the plan holds, and includes AI disclosure if the repo policy requires it. | required |



## Verdict rule
Accept (ready) if every required check passes. Reject (hold) if any required check fails. An unclear (?) grade on any required check counts as a fail.
