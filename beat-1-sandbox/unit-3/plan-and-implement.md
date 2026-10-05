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

SiddharthGarlapati

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-5985725444

I reproduced issue #68 and traced the failure to `KeywordSearcher.index([])` passing an empty tokenized corpus to `BM25Okapi`, which then raises a `ZeroDivisionError` while calculating the average document length.

My plan is to keep the change scoped to the empty-index behavior in `rag/retriever/keyword_search.py` and the existing regression test in `tests/unit/test_keyword_search.py`.

I will:
- handle the empty corpus before constructing `BM25Okapi`;
- preserve the existing behavior for non-empty corpora;
- update the existing `test_empty_index` test so it passes normally instead of remaining an expected failure.

I will verify the fix by re-running the same Unit 2 reproduction and the keyword-search unit tests. After the change, `KeywordSearcher.index([])` should complete without raising `ZeroDivisionError`, and the existing non-empty keyword-search behavior should continue to pass.

I am not planning any changes to `rank-bm25`, the BM25 ranking algorithm, other retrievers, or unrelated APIs.

---

## Your branch

**Branch**

fix/68-empty-keyword-index

**Evidence**

### Before

The existing empty-index test was run with:

```bash
pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -vv -rxX
```

Output:

```text
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index XFAIL
(issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index)

1 xfailed in 0.25s
```

The direct reproduction was:

```bash
python - <<'PY'
from rag.retriever.keyword_search import KeywordSearcher

searcher = KeywordSearcher()
searcher.index([])
PY
```

Output:

```text
Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
  File "rag/retriever/keyword_search.py", line 25, in index
    self.bm25 = BM25Okapi(tokenized_corpus)
  File "rank_bm25.py", line 52, in _initialize
    self.avgdl = num_doc / self.corpus_size
ZeroDivisionError: division by zero
```

### After

The direct reproduction was re-run after the fix:

```bash
python - <<'PY'
from rag.retriever.keyword_search import KeywordSearcher

searcher = KeywordSearcher()
searcher.index([])
PY
```

Output:

```text
2026-10-04 22:41:32 [info     ] keyword_index_built            chunk_count=0
```

The empty-index regression test was re-run with:

```bash
pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -vv
```

Output:

```text
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index PASSED [100%]

============================================ 1 passed in 0.27s ============================================
```

The complete keyword-search unit-test file was also run:

```bash
pytest tests/unit/test_keyword_search.py -vv
```

Output:

```text
collected 17 items

tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_sorted_by_score_descending PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_query_matching_no_documents PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_query_matching_multiple_documents PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_case_insensitive_matching PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_top_k_limit PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_top_k_larger_than_results PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_have_bm25_score PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_preserve_chunk_fields PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_index_not_called_returns_empty PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_multi_word_query PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_tokenization PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_tokenization_case_handling PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_large_corpus PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_special_characters_in_query PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_exact_phrase_matching PASSED
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_single_word_chunks PASSED

=========================================== 17 passed in 0.14s ============================================
```

## Eval iterations

**Run history**

Full run 1:

```text
agreement: 19/20 scored items  (bar: 18/20: PASS)
```

All required categories had at least one matching package.

Full run 2, saved to `eval-run.txt`:

```text
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

The category results in the saved run were:

```text
categories: clear-accept 5/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4
```

The second full run is the final saved run and matches `eval-run.txt`.

**Package analysis**

Package: `pkg-01`

My rubric verdict: `reject`

Gold label: `reject`

The reproduction evidence says that `--debug` showed the failure occurring in argparse and that:

> "the request items are never handed to HTTPie's item parser."

The candidate plan instead diagnoses the request-item tokenizer as the root cause and says:

> "The Python-version difference is a red herring"

My `diagnosis-grounded` and `root-cause-targeted` checks are designed to reject this kind of plan because the proposed diagnosis contradicts the reproduction evidence. The reproduced failure occurs before the request items reach the tokenizer, while the plan proposes changing that tokenizer.

Therefore my rubric returned `reject`, matching the gold label.

**Check rationale**

The following check appears in my submitted `rubric.md`:

> `| diagnosis-grounded | The candidate plan's stated diagnosis read against the issue context and the repro-evidence block, especially the observed behavior, commands, and outputs. | Pass when the stated cause explains the reproduced behavior and does not contradict or ignore evidence in the repro. The diagnosis must be supported by what was actually observed rather than by an unsupported guess. | required |`

I used this check because a technically detailed plan can still be unsafe to build when its proposed cause is not supported by the reproduction. The diagnosis should follow from observed behavior rather than from how convincing or detailed the plan sounds.

I kept this check required because both full evaluation runs correctly classified all four `wrong-cause` packages:

```text
wrong-cause 4/4
```

This showed that the grounding rule was consistently catching plans whose proposed causes did not follow from their reproduction evidence.

**Trade-offs**

The rubric is intentionally conservative about unsupported certainty. That reduces the chance of accepting a plan built around an unproven assumption, but it can also reject a reasonable plan when the package does not explicitly discuss uncertainty.

The final saved run showed this trade-off on `pkg-05`:

```text
pkg-05  clear-accept  accept  reject  NO  failed: uncertainty-honest
```

I re-ran `pkg-05` together with `pkg-14` using `--only`. The partial run produced:

```text
pkg-05  clear-accept  accept  reject  NO   failed: uncertainty-honest
pkg-14  clear-accept  accept  accept  yes

agreement: 1/2 scored items
```

This showed that `pkg-14` could pass without changing the rubric, while `pkg-05` continued to expose the cost of the stricter `uncertainty-honest` check.

I accepted that trade-off rather than loosening the check after already reaching the assignment bar, because both complete runs met the required threshold and every category had at least one match. The final saved run remained:

```text
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.