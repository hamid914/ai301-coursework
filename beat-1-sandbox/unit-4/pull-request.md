# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/157

**Branch**

fix/68-bm25-empty-index

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

19/20

**Package analysis**

For `pkg-20`, my rubric decided `accept` but the gold label was `reject`. My rubric evaluated it this way because my "Standards and Comms" check successfully verified that the AI disclosure and basic template sections were filled out, but the check was not granular enough to catch the specific, subtle contributing policy violation that this package tested for the `standards-wall` category.

**Check rationale**

"Test Evidence | The test evidence read against the plan's test plan and the repo's checks | It shows the before/after results on an observable behavior AND shows the outcomes of the repo's required automated checks (make test-unit, etc.). | required" 

I wrote it this way to explicitly catch untestable claims. Without requiring observable terminal output, the grader might accept a PR where the author just vaguely claims "tests pass," leaving the maintainer without actual proof.

**Trade-offs**

By making the "Test Evidence" check require observable before/after terminal output, I give up the ability to accept a PR where the author genuinely did the testing but only summarized the results in prose. It will unconditionally hold perfectly working code just because the formatting of the proof is lazy.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
