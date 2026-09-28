# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Claim Specificity | The claim comment read against the issue description. | The comment names the specific issue context and promises an investigation or a reproduction report, rather than asserting a fix or delivery date. | required |
| Environment Record | The repro report's environment section read against the issue's target context. | The operating system, application version, and relevant dependencies are explicitly stated and align with the issue's reported environment. | required |
| Followable Steps | The reproduction steps within the repro report. | The steps provide a complete, start-to-finish sequence of actions a stranger could execute to trigger the behavior. | required |
| Behavior Alignment | The artifacts (logs, output, excerpts) in the repro report read against the issue description. | The observed behavior shown in the artifacts explicitly matches the specific error, log, or visual bug described in the issue, rather than an adjacent one. | required |
| Honest Outcome | The repro report's stated outcome compared to its provided artifacts. | The stated outcome accurately reflects the evidence (including an honest cannot-reproduce if applicable) without confident assertions of unbacked claims. | required |
| Repo Conventions | Both candidate comments read against the `CONTRIBUTING.md` policies in the repo-facts block. | The comments respect the repository's stated contribution policies, explicitly including any mandatory AI-use disclosure requirements. | required |

## Verdict rule

Accept if every required check passes; preferred checks never change the verdict; unclear counts as fail.
