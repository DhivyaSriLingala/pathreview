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

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/DhivyaSriLingala/pathreview/commit/66d88ee

**Reproduction summary:**
I ran the targeted `test_query_with_partial_overlap` test and reproduced the failure consistently. The relevance scorer returned `1.0` because all four query tokens occur in the fixture text, causing the test's expected middle-range assertion to fail.

**PLAN.md link:** https://github.com/DhivyaSriLingala/pathreview/blob/test/157-partial-overlap-fixture/PLAN.md

**Walkthrough video (recommended):** Not recorded; this optional item is not graded.

**Blockers or open questions:**
No current blockers. The evidence indicates that the test fixture should change while the production relevance-scoring implementation remains unchanged.

## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
I completed every implementation sub-task from `PLAN.md` and opened draft PR
[#343](https://github.com/ascherj/pathreview/pull/343). The partial-overlap
fixture now shares exactly two of the query's four unique tokens, producing a
deterministic score of `0.5`; the targeted test passes, and all 19 relevance
scorer tests pass.

**Next steps:**
I will request peer or mentor feedback on the draft PR, address any actionable
feedback, mark the PR ready for review, and complete Check-in 2 with the final
validation results.

**Blockers:**
Peer or mentor review is pending. Repository-wide validation has 182
pre-existing lint errors and 52 pre-existing unit-test failures after this
fix; the contribution introduced no new failures and removed the issue #157
failure from the baseline of 53.

---
