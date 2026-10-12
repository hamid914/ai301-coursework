# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->
1. Read the `repo facts` and `issue context` to understand the rules and bug.
2. Read the `plan` (and deviations) to understand what was promised.
3. Read the `diff` to see what was actually changed. Reading the plan before the diff is critical for side-by-side fidelity checks.
4. Read the `test evidence` to verify proof.
5. Read the `PR description` to verify communication and template use.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->
1. Use `references/evidence-guide.md` to map where to find evidence for each check.
2. Perform side-by-side pairings: compare the `diff` directly against the `plan scope` to check fidelity; compare `test evidence` against the `plan test plan` and repo checks.
3. In eval mode, pull quotes exclusively from the bundle text.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
1. Grade every check in `rubric.md` strictly against the Pass condition.
2. Grade `pass`, `fail`, or `unclear` (use `unclear` only if evidence is absent).
3. Write a one-line justification quoting the diff, file, or description claim that decided the grade.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->
1. Apply the verdict rule from `rubric.md`.
2. Treat `unclear` grades as specified in the verdict rule.
3. If the verdict is `reject`, quote the first failing required check in rubric order as the deciding reason in the summary.
4. End strictly with the JSON block containing the item id, checks array, and the final `accept` or `reject` verdict.
