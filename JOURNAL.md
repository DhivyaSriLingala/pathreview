# PathReview Contribution Journal

## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/157

**Issue title:** Relevance scorer “partial overlap” test fixture actually has full query overlap

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
The partial-overlap unit test for the relevance scorer currently uses a query and chunk that share every query term. Because the scorer measures how many query keywords appear in the retrieved text, it correctly returns a full score of 1.0, while the test incorrectly expects a score below 0.9. The problem is confined to the fixture in `tests/unit/test_relevance_scorer.py`, rather than the scoring implementation in `rag/evaluator/relevance_scorer.py`. A successful fix will make the fixture contain only some of the query terms so the test accurately exercises partial keyword overlap.

**Selection reasoning:**
This issue is appropriate for my first contribution because it is a clearly defined Tier 1 problem limited to one test fixture. The issue supplies a direct reproduction command, and the existing scorer implementation makes the expected behavior straightforward to verify. It does not require database changes, external API access, or changes across multiple application layers. I also confirmed that the issue was open, unassigned, had no comments, and had no competing claim when I selected it.

**Branch name:** test/157-partial-overlap-fixture

**Setup confirmation:** [ ] App runs locally at localhost:5173

**Cohort ledger:** [ ] Issue added to cohort ledger
