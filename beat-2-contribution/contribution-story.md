# Contribution: Add unit tests for the Duration class

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Hamid Rouhani
**GitHub Username:** hamid914
**Issue:** https://github.com/hiero-ledger/hiero-sdk-python/issues/2557
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

### Unit 5: Upgrading Issue-Select to Issue-Scout and Building GitHub Search Funnels

I expanded the unit 1 issue-select skill into issue-scout by adding live GitHub
CLI search queries filtered by language, open state, and community engagement
signals. During initial test scans across wide queries, the ranking stage
repeatedly clustered multiple sub-issues from the same repository and surfaced
several low-star solo projects, while the rubric successfully intercepted and
rejected heavily contested tickets with abandoned attempts. To address this, I
tuned the search strategy filters to prioritize active, unassigned repositories
and added a deduplication rule to ensure candidate variety before final rubric
grading.

### Unit 6: Automated PreToolUse Voice Guard and Scoped Repository Memory

I deployed voice-guard as a Claude Code PreToolUse hook running check_voice.py
against my canonical voice-guide.md, ensuring outgoing GitHub comments satisfy
tone, scope, and timeline constraints. Early manual checks intercepted an
initial claim draft for using vague delivery estimates rather than concrete
investigation steps and missing the repository's mandatory `/assign` command. I
resolved this by enforcing explicit timeline wording and required bot commands
in claim-draft.md, while adding CLAUDE.local.md excluded via .git/info/exclude
to preserve test runner conventions across sessions without polluting the
repository diff.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I selected this issue from the AI301 Issue Selection site after screening
candidates across Python repositories. My scout evaluated this ticket alongside
`emfcamp/Website#1075` and `Snapchat/GiGL#169`. Using the patched scope rubric,
the scout issued an `accept` verdict with a difficulty rating of
`straightforward`. It confirmed the repository is actively maintained (commits
within 24 hours), unassigned after stale claimants were cycled out by automated
maintenance bots, and strictly bounded to adding unit tests without touching
production code.

This issue fits my background well because it focuses on Python test suite
development (`pytest`) and verifying class contracts without introducing domain
dependencies or non-deterministic behavior. I want to contribute to an active
open-source SDK while working through its testing infrastructure, dataclass
validations, and pre-commit contribution standards (such as GPG/DCO signing). 

The scout accurately distinguished this bounded task from contested or tracking
issues, though manual verification remained necessary to identify the
repository's explicit requirement for the `/assign` command in claim comments.

Claim comment: https://github.com/hiero-ledger/hiero-sdk-python/issues/2557#issuecomment-6742162800

**Toolkit**

- Tool: issue-scout (search strategy, patched rubric),
- What it produced: An accept verdict rating the issue straightforward, confirming active maintainer commits, unassigned status, and test-only scope.
- Difficulties: The scout's initial binary scope check was too rigid for wild repositories, and broad ranking initially allowed contested issues through.
- What changed: Patched the rubric with the scope-feasible check and three-tier difficulty rating (straightforward, moderate, ambitious).

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
