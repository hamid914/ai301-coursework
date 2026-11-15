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
**Pull Request:** https://github.com/hiero-ledger/hiero-sdk-python/pull/2793

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

**Unit 7: Automated PR Gatekeeping and Manifest Checks**

I installed the ship-gate hook and created a manifest to run `uv run pytest tests/unit/` and `uv run pre-commit run --all-files` on my branch before allowing a PR. During my first run, my `pr-precheck` skill intercepted the ship-gate because my test plan promised string representation tests, but my diff lacked `__str__` and `__repr__` tests. I patched my branch to include those two tests to restore plan fidelity, updated my test evidence, and the gate passed my branch.

**Unit 8: Monitoring PR Status with PR-Monitor and Playbook**

I installed the `pr-monitor` skill to track my open PR and drafted a `playbook.md` establishing a 7-day staleness threshold and direct response rules. Running `monitor.py --state` successfully read my PR's status, but since it was just opened, the monitor drafted a "note to wait" advising me to hold off on pinging the maintainers. I reviewed the drafted note and chose to hold my position without posting, keeping the thread clean while the repository's CI checks complete.

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

The `Duration` class in `src/hiero_sdk_python/Duration.py` lacks a dedicated unit test suite. Since `hiero-sdk-python` uses `pytest`, the test runner expects a corresponding `tests/unit/duration_test.py` file to verify the class's behavior, which is currently missing.

**Proposed Solution**

I will create `tests/unit/duration_test.py` to thoroughly test the `Duration` class. I will write test cases covering its initialization, property access (`seconds`), equality comparisons (specifically ensuring `__eq__` returns `False` for non-Duration objects), string representation, and protobuf conversion methods (`_to_proto` and `_from_proto`, including pinning down the `ValueError` guard). I will deliberately not alter any production code.

**Implementation Plan**

1. Create the `tests/unit/duration_test.py` file.
2. Import `Duration` and `pytest`.
3. Add tests for standard initialization and property access (observing `assert Duration(seconds=5).seconds == 5`).
4. Add tests for equality, specifically observing that `Duration(seconds=5) != "Not a Duration"` correctly evaluates to `True`.
5. Add tests for string representation (`__str__` and `__repr__`).
6. Add tests for `_to_proto` and `_from_proto`, specifically observing that `pytest.raises(ValueError)` triggers when `_from_proto` receives invalid input.
7. Run `uv run pytest tests/unit/duration_test.py` to confirm the new test behaviors pass.

**Toolkit**

- Tool: plan-check (wild scope)
- What it produced: An accept verdict on `plan.md` and `plan-comment.md`.
- Difficulties: The first plan was rejected for misnaming methods (`to_proto` instead of `_to_proto`), hallucinating a `nanos` property, omitting specific edge-case validations requested by the issue, and using a generic "run the test suite" verification step. 
- What changed: Updated the plan to use exact method names, test the specific `ValueError` and `__eq__` behaviors requested, and explicitly state the observable assertions the tests will make.

---

## Testing Strategy

I will run `uv run pytest tests/unit/duration_test.py` to verify my new test suite passes. I will then run the full unit test suite via `uv run pytest tests/unit/` and the repository's linting hooks via `uv run pre-commit run --all-files` to prove my additions do not break existing coverage or formatting rules.

**Toolkit**

- Tool: pytest and pre-commit
- What it produced: Terminal output proving 13 passed tests in `duration_test.py` and successful formatting checks across the repository.
- Difficulties: The test runner initially crashed during collection (`ModuleNotFoundError`) because the HAPI protobuf files were not compiled.
- What changed: I executed `generate_proto.py` via `uv` to download and compile the Hedera protobufs locally, enabling pytest to run successfully.

---

## Implementation Notes

**2026-11-14**
Generated `hiero_sdk_python.hapi` protobufs using `generate_proto.py`. Created branch `fix/2557-duration-tests`. Implemented `tests/unit/duration_test.py` with 13 tests covering initialization, string representation, `__eq__` false-conditions, and protobuf serialization including the `ValueError` guard.

**Toolkit**
- Tool: claude code (implementation)
- What it produced: The `duration_test.py` file, generated from the approved `plan.md`.
- Difficulties: The initial Claude-generated file imported `Duration` using a lowercase filename (`duration.py`), which caused an import error on my local filesystem.
- What changed: Claude corrected the import to use the exact PascalCase filename (`Duration.py`) identified during my reproduction phase.

---

## Pull Request

**PR Link:** https://github.com/hiero-ledger/hiero-sdk-python/pull/2793

**PR Description:** Fixes #2557. Created `tests/unit/duration_test.py` to add dedicated unit test coverage for the `Duration` class. Verified standard initialization, the `seconds` property, equality behavior (including `__eq__` returning `False` for non-Duration objects), and protobuf serialization (`_to_proto` and `_from_proto`), including the `ValueError` guard. Included full before-and-after terminal evidence and a natural AI-assistance disclosure respecting the repository's bot policy.

**Maintainer Feedback:**

- 2026-11-15: none yet

**Status:** Awaiting review

**Toolkit**

- Tool: ship-gate, voice-guard, and Claude Code (gh cli)
- What it produced: An automated validation of the branch against my manifest and test plan, followed by the final PR submission to GitHub.
- Difficulties: The ship-gate caught that the global `pytest` command failed due to missing dependencies, and the `pr-precheck` caught that my branch was missing the `__str__` tests promised in my plan. Later, the voice-guard blocked the PR creation because my draft evidence was stale (showing 11 dots in the full suite instead of the updated 13).
- What changed: I scoped the manifest's test command to `tests/unit/`, added the missing string representation tests to my branch, and refreshed the full-suite test evidence to match the new 13-test count before the hooks allowed the PR to open.

---

## Learnings and Reflections

**Technical Skills Gained**

Mastering `uv` for Python dependency management and lockfile isolation; understanding Protocol Buffer compilation (`generate_proto.py`) within a large SDK; testing Python dataclasses and properties using `pytest`, including validating specific exceptions with `pytest.raises(ValueError)`.

**Challenges Overcome**

I overcame an initial `ModuleNotFoundError` during pytest collection by locating and executing the repository's HAPI protobuf compilation script to build missing dependencies. Later, I passed strict `ship-gate` requirements by recovering from a corrupted `pre-commit` hook cache and patching my branch to include `__str__` tests that were promised in my plan but missed in my initial implementation.

**What I'd Do Differently Next Time**

I would scope my test runner command (`uv run pytest tests/unit/`) earlier in the reproduction phase to avoid confusion from global test suites that inherently fail on `main` due to uninstalled optional extras (like Flask for the TCK suite).

---

## Resources Used

- Hiero SDK Python `CONTRIBUTING.md` for formatting and DCO sign-off rules.
- CodeRabbit's plan comment on issue #2557 for scoping the required edge-case test validations.
- Pytest documentation for the `pytest.raises` exception testing syntax.
