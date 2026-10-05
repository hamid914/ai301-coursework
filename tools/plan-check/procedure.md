# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->
1. Read the `issue context` and thread highlights first to understand the bug, the repository's rules, and any explicit maintainer constraints.
2. Read the `repro evidence` carefully to understand the exact behavior and steps that the plan must fix.
3. Read the `candidate plan` (or `plan.md` in live mode) to evaluate the proposed diagnosis, scope, approach, and test plan.
4. Read the `candidate plan comment` (or `comment.md` in live mode) to see how the plan is communicated upstream.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->
1. Open `references/evidence-guide.md` and use it as a map to find where the evidence for each check in `rubric.md` lives.
2. For the Diagnosis and Test Plan checks, you must gather evidence from the plan and explicitly compare it against the `repro evidence` to ensure they match.
3. In eval mode, pull quotes and facts strictly from the provided markdown bundle text. Do not fetch external links.
4. In live mode, gather evidence from the live GitHub issue URL and the student's draft files (`plan.md` and `comment.md`).

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
1. Execute every check listed in `rubric.md` one by one.
2. For each check, strictly apply the "Pass condition" to the evidence you gathered. Do not grade based on formatting, length, or gut feel.
3. Grade the check `pass`, `fail`, or `unclear`. Grade `unclear` only if the required evidence is genuinely missing from the package.
4. Record a one-line justification for each grade, quoting the specific fact, line, or contradiction from the package that decided the outcome.
5. In live mode only, read `voice-guide.md` and note any communication rules broken by the draft plan comment.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
1. Read the "Verdict rule" defined below the table in `rubric.md`.
2. Apply the rule to your check grades to determine the final verdict: `accept` (ready to post and build from) or `reject` (hold).
3. If the verdict rule does not specify how to handle an `unclear` grade, treat `unclear` as a `fail` (proof you cannot verify is proof you cannot build from).
4. Output a short readable summary of the grades and justifications.
5. End your response strictly with the required fenced JSON block containing the item id, the checks array (name, grade, evidence), and the final `accept` or `reject` verdict.
