# Plan — Issue #68

## Diagnosis

The reproduced failure occurs when `KeywordSearcher.index([])` receives an empty corpus.

The direct reproduction showed:

```python
searcher = KeywordSearcher()
searcher.index([])
```

and produced:

```text
ZeroDivisionError: division by zero
```

The traceback shows the failure path:

```text
File "rag/retriever/keyword_search.py", line 25, in index
    self.bm25 = BM25Okapi(tokenized_corpus)

File "rank_bm25.py", line 52, in _initialize
    self.avgdl = num_doc / self.corpus_size

ZeroDivisionError: division by zero
```

The empty corpus is tokenized and passed directly to `BM25Okapi`. During initialization, `rank-bm25` calculates the average document length using a corpus size of zero, which causes the division-by-zero error.

The repository already has an empty-index test documenting this behavior as an expected failure:

```text
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index XFAIL
(issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index)
```

`KeywordSearcher.search()` already handles an empty state by returning an empty list, so `index([])` should also handle an empty corpus without raising an exception.

## Scope

### In scope

- Handle an empty corpus in `KeywordSearcher.index()` without passing it to `BM25Okapi`.
- Ensure the searcher remains in a valid empty-index state after `index([])`.
- Update the existing `test_empty_index` regression test so the fixed behavior is tested normally instead of remaining an expected failure.
- Verify that the original Unit 2 reproduction no longer raises `ZeroDivisionError`.

### Out of scope

- Changes to the `rank-bm25` dependency.
- Changes to the BM25 ranking algorithm.
- Changes to ranking behavior for non-empty corpora.
- Changes to other retrievers.
- Broader refactoring of the keyword-search implementation.
- API redesigns unrelated to issue #68.

## Files

The planned change is limited to:

- `rag/retriever/keyword_search.py`
- `tests/unit/test_keyword_search.py`

## Approach

1. Update `KeywordSearcher.index()` to detect an empty tokenized corpus before constructing `BM25Okapi`.

2. For an empty corpus, leave the searcher in an empty state compatible with the existing behavior of `search()`, rather than constructing `BM25Okapi` with zero documents.

3. Preserve the current `BM25Okapi` initialization path for non-empty corpora so normal keyword-search behavior remains unchanged.

4. Update `TestKeywordSearcher.test_empty_index` so it represents the fixed behavior instead of an expected failure.

5. Keep the implementation limited to the empty-index case required by issue #68.

## Test plan

### Re-run the existing empty-index test

Before the fix, Unit 2 produced:

```bash
pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -vv -rxX
```

with:

```text
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index XFAIL
(issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index)

1 xfailed
```

After the fix, run the same test again.

Expected result:

- `test_empty_index` should no longer be an expected failure.
- The test should pass normally.
- `KeywordSearcher.index([])` should not raise `ZeroDivisionError`.

### Re-run the direct reproduction

Run:

```bash
python - <<'PY'
from rag.retriever.keyword_search import KeywordSearcher

searcher = KeywordSearcher()
searcher.index([])
PY
```

Before the fix, this raised:

```text
ZeroDivisionError: division by zero
```

After the fix, the command should complete without an exception.

### Run the keyword-search unit tests

Run:

```bash
pytest tests/unit/test_keyword_search.py -vv
```

Expected result:

- the empty-index regression test passes;
- existing keyword-search tests for non-empty corpora continue to pass;
- the change does not alter normal keyword-search behavior.

## Risks and unknowns

- The empty-index handling must leave the searcher in a valid state for a later call to `search()`.
- If `index([])` is called after a previous non-empty index, the implementation must not accidentally preserve stale BM25 data from the previous corpus.
- The fix should not change BM25 initialization or ranking behavior when the corpus is non-empty.
- The exact empty-state representation should follow the existing `KeywordSearcher` implementation rather than introducing a new public API or unrelated state model.

## Deviations

Nothing changed during implementation; the build followed the plan as written.