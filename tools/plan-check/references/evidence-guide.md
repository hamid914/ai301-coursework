# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->
- Where it lives: Look at the "Candidate plan" (specifically the Diagnosis or Cause section) and compare it directly to the "Repro evidence" block (specifically the steps and actual behavior). In live mode, compare `plan.md` to the student's posted repro comment.
- What good looks like: The stated root cause explicitly explains the behavior proven in the repro evidence. It does not contradict the evidence or blame a module/symptom that the reproduction already ruled out.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->
- Where it lives: Look at the "Candidate plan" (specifically the Scope, Change, or In/Out sections).
- What good looks like: The plan names the exact files or functions it will modify (e.g., `pkg/gui/controllers/sync_controller.go`) AND explicitly states what it will *not* touch (e.g., "Out: any change to how push status is computed") to prevent scope creep.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->
- Where it lives: Look at the "Candidate plan" (specifically the Approach, Change, or Implementation steps).
- What good looks like: The plan provides a concrete technical approach and names specific files so a stranger could start coding it immediately. It is not just a vague promise to "investigate", "poke around", or "figure it out".

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->
- Where it lives: Look at the "Candidate plan" (specifically the Test section) and compare it against the steps in the "Repro evidence" block.
- What good looks like: The test plan involves re-running the exact repro steps, but it states a clear, observable expected outcome after the fix (e.g., "at step 3 the color must flip without leaving the view"). It must not vaguely say "run the test suite" or "see if it works".

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->
- Where it lives: Look at the "Candidate plan" (specifically the Risks, Unknowns, or Deviations sections).
- What good looks like: The plan explicitly notes what is uncertain, untested, or deferred, rather than faking 100% certainty. In live mode, if the built code differs from the plan, those differences are explicitly recorded under a `## Deviations` header in `plan.md`.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->
- Where it lives: Look at the "Candidate plan comment" (or `comment.md` in live mode) and compare it against both the "Thread highlights" and the "Repo facts" (specifically the contribution/AI policy).
- What good looks like: The comment only promises what is actually in the plan. It directly engages with any maintainer constraints mentioned in the thread (e.g., "keeping it minimal given the review-bandwidth note in CONTRIBUTING") and includes an AI-usage disclosure if the repo policy requires one.
