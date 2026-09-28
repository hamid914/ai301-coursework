# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment
- Where it lives: The beginning of the repro report or a dedicated environment section. In live mode, read this against the original issue's reported system parameters.
- What good looks like: The exact operating system, software version, and dependency versions are listed. The versions match what the issue targets, or the difference is explicitly called out.

## Steps
- Where it lives: The main body of the repro report.
- What good looks like: An ordered, unbroken sequence of commands or interface actions starting from a fresh state that reliably triggers the reported behavior.

## Behavior shown
- Where it lives: The logs, terminal output excerpts, or screenshots included in the repro report.
- What good looks like: The provided artifacts capture the exact failure mode, error message, or visual bug the original reporter described, proving the specific issue was triggered.

## Honesty
- Where it lives: The comparison between the report's text claims and the backing artifacts.
- What good looks like: The report states exactly what happened. An evidenced cannot-reproduce is stated plainly, and the report does not claim more than the artifacts prove.

## Comms
- Where it lives: The claim comment, repro report text, and the repo-facts block (specifically `CONTRIBUTING.md` policies).
- What good looks like: The language is specific to the issue and honest. If the repository requires AI-assistance disclosure, the comments explicitly include it.
