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

**Unit 5: Upgrading Issue-Select to Issue-Scout and Building GitHub Search Funnels**

I expanded the unit 1 issue-select skill into issue-scout by adding live GitHub
CLI search queries filtered by `--state open --no-assignee` and language tags.
During initial test scans across wide queries, the ranking stage repeatedly
clustered multiple sub-issues from the same repository (such as `SKaiNET#1380`
and `SKaiNET#1372`) and surfaced 0-to-2-star solo projects like `leaklens`. To
solve this, I added a deduplication rule limiting candidates to at most one per
repository and introduced a ranking preference for active repositories with
over 10 stars before grading against rubric.md.

**Unit 6: Automated PreToolUse Voice Guard and Scoped Repository Memory**

I deployed voice-guard as a Claude Code PreToolUse hook running check_voice.py against my canonical voice-guide.md, ensuring outgoing comments satisfy tone, scope, and timeline constraints. Early manual checks intercepted an initial claim draft for using vague delivery estimates rather than concrete investigation steps and missing the repository's mandatory `/assign` command. I resolved this by enforcing explicit timeline wording and required bot commands in claim-draft.md, while adding CLAUDE.local.md excluded via .git/info/exclude to preserve test runner conventions across sessions without polluting the repository diff.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I selected this issue from the AI301 Issue Selection site after screening candidates across Python repositories. My scout evaluated this ticket alongside `emfcamp/Website#1075` and `Snapchat/GiGL#169`. Using the patched scope rubric, the scout issued an accept verdict with a difficulty rating of straightforward. It confirmed the repository is actively maintained (commits within 24 hours), unassigned after stale claimants were cycled out by automated maintenance bots, and strictly bounded to adding unit tests without touching production code.

This issue fits my background well because it focuses on Python test suite development (pytest) and verifying class contracts without introducing domain dependencies or non-deterministic behavior. I want to contribute to an active open-source SDK while working through its testing infrastructure, dataclass validations, and pre-commit contribution standards (such as GPG/DCO signing).

The scout accurately distinguished this bounded task from contested or tracking issues, though manual verification remained necessary to identify the repository's explicit requirement for the `/assign` command in claim comments.

Claim comment: https://github.com/hiero-ledger/hiero-sdk-python/issues/2557#issuecomment-6742162800

**Toolkit**

- Tool: issue-scout (search strategy, patched rubric)
- What it produced: An accept verdict rating the issue straightforward, confirming active maintainer commits, unassigned status, and test-only scope.
- Difficulties: The scout's initial binary scope check was too rigid for wild repositories, and broad ranking initially allowed contested issues through.
- What changed: Patched the rubric with the scope-feasible check and three-tier difficulty rating (straightforward, moderate, ambitious).

---

## Understanding the Issue

**Problem Description**

The `hiero-sdk-python` library provides the `Duration` class under `src/hiero_sdk_python/Duration.py` to represent Hedera network time durations and handle conversions to and from Protobuf objects. While sibling types like `AccountId` and `Timestamp` have thorough test coverage, `Duration` currently lacks any dedicated unit tests in `tests/unit/duration_test.py`.

**Expected Behavior**

A dedicated test suite `tests/unit/duration_test.py` should exist, testing all public methods and properties of `Duration`: initialization with valid and invalid types, equality checks (`__eq__`), string representation (`__str__`), property accessors, protobuf serialization (`to_proto`), and deserialization (`from_proto`).

**Current Behavior**

The file `tests/unit/duration_test.py` is missing entirely from the repository. Invoking `pytest tests/unit/duration_test.py` fails with `ERROR: file or directory not found`.

**Affected Components**

* `src/hiero_sdk_python/Duration.py`: Source code defining the `Duration` class under test.
* `tests/unit/duration_test.py`: The missing test module to be created.
* Sibling references for conventions: `tests/unit/account_id_test.py` and `tests/unit/timestamp_test.py`.

**Toolkit**

- Tool: repo exploration and code inspection via Neovim and bash
- What it produced: Located the source file at `src/hiero_sdk_python/Duration.py` and confirmed `tests/unit/duration_test.py` does not exist.
- Difficulties: The issue body referenced `src/hiero_sdk_python/duration.py` in lowercase, but the actual repository file uses PascalCase `Duration.py`.
- What changed: Verified the exact PascalCase import path (`from hiero_sdk_python.Duration import Duration`) to avoid import errors in test authoring.

---

## Reproduction Process

**Environment Setup**

- Operating System: Arch Linux x86_64
- Language & Runtime: Python 3.12
- Package & Environment Manager: uv
- Test Framework: pytest
- Cloned Repository: fork at `https://github.com/hamid914/hiero-sdk-python`
- Setup Commands:
```bash
git clone https://github.com/hamid914/hiero-sdk-python.git
cd hiero-sdk-python
uv sync
```


* Challenges Faced: Initial attempt to run `uv pip install -e ".[dev]"` yielded a warning because the repository manages dependencies via `uv.lock` rather than package extras. Using `uv sync` cleanly configured the environment and installed pytest.

**Steps to Reproduce**

1. Clone the fork repository and install dependencies:
```bash
git clone https://github.com/hamid914/hiero-sdk-python.git
cd hiero-sdk-python
uv sync
```


2. Verify that the class under test exists:
```bash
ls src/hiero_sdk_python/Duration.py
```


3. Run the unit test target:
```bash
uv run pytest tests/unit/duration_test.py
```



**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:**
```text
$ uv run pytest tests/unit/duration_test.py
ERROR: file or directory not found: tests/unit/duration_test.py
```


- **My findings:** The `Duration` class implementation is present in `src/hiero_sdk_python/Duration.py`, but `tests/unit/duration_test.py` does not exist. Running pytest directly confirms the missing file.

**Toolkit**

- Tool: repro-check (wild scope)
- What it produced: An accept verdict on `claim-draft.md` and `repro-draft.md` for issue #2557.
- Difficulties: The first claim draft was rejected by repro-check for promising deliverable deadlines instead of an investigation and omitting the repository's mandatory `/assign` trigger.
- What changed: Updated the claim draft to use `/assign` and state concrete local test reproduction steps instead of promised completion dates.


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
