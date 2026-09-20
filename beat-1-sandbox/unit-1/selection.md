# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68

**Verdict output**

Re-checked the live evidence — nothing has changed since the previous grade (updated_at still 2026-09-19T01:53:38Z, 1 comment, no assignee, still zero PRs in the repo, not archived, last push 2026-09-16). Same result.

- maintainer-alive — pass. Last main commit 2026-09-16 by Andrew Burke (Aburke225, COLLABORATOR), 4 days ago; recent history is all his, no bots.
- repo-in-use — pass. "archived": false, "pushed_at": "2026-09-16T21:50:20Z".
- newcomer-scope — pass. One bounded goal: stop KeywordSearcher.index() raising ZeroDivisionError on an empty corpus, mirroring how search() already handles it, and remove the xfail(H-01) marker. Two named files, maintainer-opened, good first issue + tier-1, no design debate, no abandoned attempts.
- unclaimed — pass. No assignee, no PR of any kind. The single comment is a claim by acordero4852 (author_association: NONE — a classmate) from 2026-09-19, which the Path Review house rule says does not block.
- contribution-policy — pass. docs/CONTRIBUTING.md sets workflow terms only; nothing restricting AI-assisted contributions.

Verdict: accept. Same two things to carry into the work: a classmate claimed it two days ago, so expect company (harmless for course credit — it attaches to the PR you open); and the xfail is strict=True, so removing that marker is part of the fix or CI fails once your change works.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68",
  "checks": [
    {"name": "maintainer-alive", "grade": "pass", "evidence": "Newest main commit 2026-09-16 by human collaborator Andrew Burke (Aburke225), 4 days before grading."},
    {"name": "repo-in-use", "grade": "pass", "evidence": "\"archived\": false and \"pushed_at\": \"2026-09-16T21:50:20Z\" on the repo record."},
    {"name": "newcomer-scope", "grade": "pass", "evidence": "One goal — make index([]) not raise, plus remove the xfail(H-01) marker; two named files, opened by a COLLABORATOR, labeled good first issue / tier-1."},
    {"name": "unclaimed", "grade": "pass", "evidence": "\"assignees\": [], zero PRs in the repo; sole comment is a 2026-09-19 claim by acordero4852 (author_association NONE), which the Path Review house rule says does not block."},
    {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md states workflow rules only; no mention of AI, LLM, or generated-code restrictions."}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

**Run history**

1. `agreement: 14/20 scored items (bar: 18/20: below the bar)`
2. `agreement: 3/6 scored items`
3. `agreement: 3/6 scored items`
4. `agreement: 3/6 scored items`
5. `agreement: 16/20 scored items (bar: 18/20: below the bar)`
6. `agreement: 2/4 scored items`
7. `agreement: 1/2 scored items`
8. `agreement: 2/4 scored items`
9. `agreement: 3/4 scored items`
10. `agreement: 18/20 scored items (bar: 18/20: PASS)`
11. `agreement: 18/20 scored items (bar: 18/20: PASS)`

The last score is from the complete saved run written to `eval-run.txt`.

**Issue analysis**

`issue-01  accept  reject  NO  failed: newcomer-scope`

For `issue-01`, my rubric's decision was `reject`, while the gold label was `accept`. The result came from the `newcomer-scope` check. The issue asked for several related documentation changes, including creating a new documentation page and updating other related pages. My rubric treated those multiple changes as broader scope, even though they all supported one main goal. This showed that several related changes can still form one bounded contribution.

**Check rationale**

My current `newcomer-scope` check is:

> `| newcomer-scope | Issue body, labels, linked PRs, and comment thread | Pass if the issue has one main goal. Multiple related changes, causes, or possible fixes for the same goal are allowed. A short issue can pass if it is opened by a maintainer or labeled good first issue. Fail if it is an umbrella/tracking issue, a support question, the comments show unresolved design with no maintainer-set direction, or there are 2 or more abandoned implementation attempts. | required |`

I changed the check to focus on whether the issue has one main goal rather than simply how many files, changes, causes, or possible fixes it mentions. During evaluation, some valid issues were being rejected because they contained several related changes even though they were still bounded. I kept clear failure cases such as umbrella issues, support questions, unresolved design, and repeated abandoned attempts.

**Trade-offs**

One trade-off is that allowing multiple related changes, causes, or possible fixes makes the check more permissive and can allow some technically harder issues to pass when they still appear to have one main goal.

One canary I re-ran was `issue-19`. Earlier I received:

`issue-19  accept  reject  NO  failed: newcomer-scope`

After changing the scope wording to allow multiple related causes or possible fixes for the same goal, the final full run produced:

`issue-19  accept  accept  yes`

This improved the result for `issue-19`, but the trade-off is that a difficult issue could still pass if its complexity is presented as one bounded goal.

---

## Selection rationale

**Selection rationale**

1. Issue #68 fits my interests because it is a Python RAG and retrieval bug involving keyword search. I have experience with RAG, hybrid search, and BM25, so the issue is related to concepts I already know while also giving me practice debugging an existing codebase. It is labeled `good first issue` and `tier-1`, so I expect it to fit the time available.

2. The verdict correctly identified that the repository and maintainer are active, the task has a bounded goal, there is no blocking pull request, and the contribution policy does not prohibit the AI-assisted workflow. It also correctly applied the Path Review house rule to the existing classmate claim. Outside the rubric, I considered how closely the issue matched my previous RAG and retrieval experience compared with the other accepted issues.

3. The main anticipated difficulty in claiming the issue is that another classmate has already commented that they are working on it. Normally I would be concerned about overlapping work, but the Path Review house rule says that classmate claims do not block an issue and course credit attaches to the pull request. Because of that, I can still carry issue #68 into Unit 2.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.