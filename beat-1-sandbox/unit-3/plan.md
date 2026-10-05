# Plan: Fix ZeroDivisionError on empty index in BM25 keyword search (#68)

## Repro Evidence
My plan relies on the following reproduction evidence from my Unit 2 report:
> **Steps:**
> 1. Set up a virtual environment and run `pip install -e '.[dev]'`.
> 2. Remove the `@pytest.mark.xfail` marker from `test_empty_index` in `tests/unit/test_keyword_search.py`.
> 3. Run `pytest tests/unit/test_keyword_search.py`.
> 
> **Actual behavior:** The test crashes with a `ZeroDivisionError` because the BM25 algorithm attempts to divide by the total number of documents (which is 0 when the index is empty).

## Diagnosis
The `ZeroDivisionError` explicitly matches the behavior shown in the reproduction evidence. It occurs because the code does not check if the search corpus/chunks are empty before attempting to initialize the `BM25Okapi` index, leading to a division by zero in `rank_bm25`'s `_initialize` method.

## Scope
- **In-scope:** Adding an early-return guard inside the `index()` function of the BM25 searcher to handle empty chunks gracefully.
- **Out-of-scope:** Modifying the `search()` function (which already handles the empty case), refactoring the broader search module, upgrading the `rank-bm25` dependency, or changing how populated indexes are initialized.

## Files to change
- `keyword_search.py` (specifically the `index()` function)
- `tests/unit/test_keyword_search.py` (to ensure the `xfail` marker is permanently removed)

## Approach
1. Locate the `index()` function in `keyword_search.py`.
2. Add a conditional check at the beginning of the function: if the provided chunks/corpus are empty, set `self.bm25 = None` (or the equivalent internal state), store the empty chunks, and return early without calling `BM25Okapi`.
3. Proceed with normal BM25 initialization only if the corpus has documents.

## Test Plan
I will re-run the exact steps from my reproduction:
1. Run `pytest tests/unit/test_keyword_search.py` with the `xfail` marker removed from `test_empty_index`.
2. **Expected outcome after fix:** The test suite passes successfully with exit code 0, and `test_empty_index` no longer throws a `ZeroDivisionError`.

## Risks and Unknowns
One unknown is verifying whether any other components rely on `index()` explicitly returning a specific object type rather than `None` when empty. However, the issue explicitly notes `search()` already handles the `self.bm25 = None` case safely.

## Deviations

Nothing changed; the plan held.
