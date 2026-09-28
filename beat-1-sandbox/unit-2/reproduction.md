# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

hamid914

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5864284510

I am looking into this `ZeroDivisionError` regarding the empty index in the BM25 keyword search. I will investigate the behavior and post a reproduction report shortly.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5864342397

I reproduced the `ZeroDivisionError` when the BM25 keyword search index is initialized with an empty corpus.

### Environment
- **OS:** Arch Linux
- **Python:** 3.14.7
- **pytest:** 9.1.1
- **rank-bm25:** 0.2.2
- **Code State:** `main` (commit `f89c06f`)

### Steps to Reproduce
1. Clone the repository and initialize the backing services (`cp .env.example .env` and `docker compose up -d`).
2. Create and activate a Python virtual environment: `python -m venv .venv && source .venv/bin/activate`.
3. Install the project and its development dependencies: `pip install -e ".[dev]"`.
4. Open `tests/unit/test_keyword_search.py` and remove the `@pytest.mark.xfail` decorator from the `test_empty_index` function (lines 134–137).
5. Run the specific unit test: `pytest tests/unit/test_keyword_search.py`

### Observed Behavior
The test crashes with a `ZeroDivisionError` at `self.avgdl = num_doc / self.corpus_size` inside the `rank_bm25` library, exactly as the issue describes. Here is the resulting stack trace:

```python
=================================== FAILURES ===================================
_____________________ TestKeywordSearcher.test_empty_index _____________________

self = <tests.unit.test_keyword_search.TestKeywordSearcher object at 0x7ff6127ae950>
searcher = <rag.retriever.keyword_search.KeywordSearcher object at 0x7ff6127af650>

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

self = <rank_bm25.BM25Okapi object at 0x7ff615954550>, corpus = []

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
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

agreement: 19/20 scored items  (bar: 18/20: PASS)

**Package analysis**

`pkg-12`. The gold label for this package was "accept", but my rubric evaluated it as a "reject". My rubric rejected it specifically because it failed the "Followable Steps" check. The rubric evaluated the package this way because it lacked a strict, unbroken sequence of commands or actions starting from a fresh state, which my rubric required for a passing grade.

**Check rationale**

> Check: Followable Steps
> Evidence: The reproduction steps within the repro report.
> Pass condition: The steps provide a complete, start-to-finish sequence of actions a stranger could execute to trigger the behavior.
> Weight: required

This check reads this way to strictly enforce that a stranger can execute the steps without guessing or inferring missing context. I rejected looser definitions of "steps" (like conversational descriptions) in favor of this rigid condition to guarantee reproducibility.

**Trade-offs**

By strictly requiring a "start-to-finish sequence of actions," the Followable Steps check successfully gates poorly written reports, which allowed the rubric to correctly catch 3 out of 3 packages in the `unfollowable-comms` category. The explicit trade-off is that this strictness results in false negatives on borderline packages like `pkg-12`, where a human maintainer might accept the report by inferring the missing context, but the programmatic check rejects it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
