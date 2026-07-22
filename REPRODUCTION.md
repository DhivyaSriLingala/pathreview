# Issue #157 Reproduction

## Environment

- Branch: `test/157-partial-overlap-fixture`
- Python: 3.11
- Test file: `tests/unit/test_relevance_scorer.py`
- Implementation: `rag/evaluator/relevance_scorer.py`

## Reproduction command

```bash
.venv/Scripts/pytest tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap -q
```

## Observed behavior

The test fails at `assert 0.3 < score < 0.9` because `score` is `1.0`.
The query is `Python Django web framework`, and the fixture text is
`Django is a Python web framework for rapid development`. All four query
tokens occur in the fixture text, so the scorer correctly calculates full
keyword coverage rather than partial overlap.

## Expected behavior

The fixture should omit at least one query token while retaining enough shared
tokens to produce a score strictly between `0.3` and `0.9`. The production
scoring implementation should remain unchanged because its current result is
correct for the supplied input.

## Scope

The defect is in the `test_query_with_partial_overlap` fixture in
`tests/unit/test_relevance_scorer.py`. It is not a defect in
`RelevanceScorer.score()` in `rag/evaluator/relevance_scorer.py`.
