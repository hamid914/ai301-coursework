# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer contribution in issues | comment thread | A maintainer has commented within the last 30 days, OR the last default-branch commit was within 90 days | required |
| Latest release date | repo-facts block | The last push to any branch or latest default-branch commit is within the last 6 months | required |
| Fully AI usage is not allowed | repo-facts block | The contribution policy does not explicitly ban AI-generated contributions | required |
| Claimed check | repo-facts block and comment thread | The issue has no assignee and no open linked PRs | required |
| Scope check | issue body, comment thread, and repo-facts block | The issue describes a well-defined, bounded piece of work with a settled specification. It is not an open-ended feature wish, tracking list, or umbrella issue. The design is not actively being debated, and it does not have a history of several abandoned (closed, unmerged) PRs. (Note: Checklists, multiple causes, or suggested fixes for a single bug are acceptable) | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept only if all required checks pass; preferred checks never change the verdict but only rank accepted issues; unclear counts as fail.
