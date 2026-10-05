# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

hamid914

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5988229932

Following up on [my reproduction above](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5864342397), the `ZeroDivisionError` occurs during `BM25Okapi` initialization because it attempts to divide by zero when the corpus is empty.

Per the note in the issue description that `search()` already handles the empty case safely, my plan keeps the fix strictly within `index()`. I will add a guard in `index()` to set `self.bm25 = None` and return early if the chunks are empty, avoiding the `BM25Okapi` call entirely. I'll verify this by ensuring the `test_empty_index` test passes successfully after removing its `xfail` marker.

Per the repository's AI policy, I am using AI assistance to help draft this fix, and I will be personally reviewing and driving the changes. I am preparing the code branch and test evidence next.

---

## Your branch

**Branch**

fix/68-bm25-empty-index

**Evidence**

**BEFORE FIX (Repro Steps):**
% pytest tests/unit/test_keyword_search.py
============================= test session starts ==============================
platform linux -- Python 3.14.7, pytest-9.1.1, pluggy-1.6.0
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: platformdirs-4.12.1, hypothesis-6.168.2, anyio-4.15.1, pytest_httpserver-1.1.5, cov-7.1.0, benchmark-5.3.0, asyncio-1.4.0
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 17 items

tests/unit/test_keyword_search.py ........F........                      [100%]

=================================== FAILURES ===================================
_____________________ TestKeywordSearcher.test_empty_index _____________________

self = <tests.unit.test_keyword_search.TestKeywordSearcher object at 0x7f5aac9a2650>
searcher = <rag.retriever.keyword_search.KeywordSearcher object at 0x7f5aac9a3350>

    def test_empty_index(self, searcher):
        """Test searching on empty index."""
>       searcher.index([])

tests/unit/test_keyword_search.py:140: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
rag/retriever/keyword_search.py:25: in index
    self.bm25 = BM25Okapi(tokenized_corpus)
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^
.venv/lib/python3.14/site-packages/rank_bm25.py:83: in __init__
    super().__init__(corpus, tokenizer)
.venv/lib/python3.14/site-packages/rank_bm25.py:27: in __init__
    nd = self._initialize(corpus)
         ^^^^^^^^^^^^^^^^^^^^^^^^
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 

self = <rank_bm25.BM25Okapi object at 0x7f5aaf5c4550>, corpus = []

    def _initialize(self, corpus):
        nd = {}  # word -> number of documents with word
        num_doc = 0
        for document in corpus:
            self.doc_len.append(len(document))
            num_doc += len(document)
    
            frequencies = {}
            for word in document:
                if word not in frequencies:
                    frequencies[word] = 0
                frequencies[word] += 1
            self.doc_freqs.append(frequencies)
    
            for word, freq in frequencies.items():
                try:
                    nd[word]+=1
                except KeyError:
                    nd[word] = 1
    
            self.corpus_size += 1
    
>       self.avgdl = num_doc / self.corpus_size
                     ^^^^^^^^^^^^^^^^^^^^^^^^^^
E       ZeroDivisionError: division by zero

.venv/lib/python3.14/site-packages/rank_bm25.py:52: ZeroDivisionError
=========================== short test summary info ============================
FAILED tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index
========================= 1 failed, 16 passed in 0.37s =========================

**AFTER FIX:**

% pytest tests/unit/test_keyword_search.py
============================= test session starts ==============================
platform linux -- Python 3.14.7, pytest-9.1.1, pluggy-1.6.0
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: platformdirs-4.12.1, hypothesis-6.168.2, anyio-4.15.1, pytest_httpserver-1.1.5, cov-7.1.0, benchmark-5.3.0, asyncio-1.4.0
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 17 items

tests/unit/test_keyword_search.py .................                      [100%]

============================== 17 passed in 0.33s ==============================

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

19/20

**Package analysis**

For `pkg-01`, my rubric decided `reject` and the gold label was `reject`. My rubric correctly read it this way because the "Diagnosis Grounding" check failed it. The plan in `pkg-01` blamed the request-item tokenizer, but the package's own control run parsed fine without the `-v` flag, which ruled the tokenizer out entirely. The rubric's requirement that the diagnosis must "explicitly explain the behavior shown in the reproduction evidence without contradicting or ignoring it" caught this ungrounded cause.

**Check rationale**

"Decisive Test Plan | The plan's test section read against the repro-evidence block | It states an observable expected outcome (e.g., expected terminal output) rather than a vague "run the test suite" or "see if it works". | required"

This check reads this way to explicitly catch untestable plans. I wrote it to force the planner to define exactly what observable change proves the fix worked. Without the "observable expected outcome" requirement, the grader would accept vague test plans like the one in `calib-04`, which just said "run the full test suite" without specifying what the suite should actually output to prove the specific bug is gone.

**Trade-offs**

By making the "Decisive Test Plan" check so strict about requiring an explicitly stated observable outcome (like terminal output), I give up the ability to accept plans that are technically correct in their approach but lazy in their test description. A maintainer might be perfectly fine accepting a plan that says "I'll run the test suite to ensure no regressions" if the code fix is obvious. My check will unconditionally hold those plans, forcing the author to rewrite their test plan even if the code approach was already perfect.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
