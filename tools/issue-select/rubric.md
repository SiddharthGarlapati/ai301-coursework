# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | Last 5 default-branch commits and maintainer response sample in the repo-facts block | Pass if there is human maintainer activity within the last 90 days. | required |
| repo-in-use | Archived status, last push, and last 5 default-branch commits in the repo-facts block | Pass if the repo is not archived and has activity within the last 90 days. | required |
<!-- | newcomer-scope | Issue body, labels, linked PRs, and comment thread | Pass if the issue has one bounded goal. Multiple related changes for the same goal are allowed. A short issue can pass if it is opened by a maintainer or labeled good first issue. Fail if it is an umbrella/tracking issue, a support question, has unresolved design, or has 2 or more abandoned implementation attempts such as closed unmerged PRs. | required | -->
| newcomer-scope | Issue body, labels, linked PRs, and comment thread | Pass if the issue has one main goal. Multiple related changes, causes, or possible fixes for the same goal are allowed. A short issue can pass if it is opened by a maintainer or labeled good first issue. Fail if it is an umbrella/tracking issue, a support question, the comments show unresolved design with no maintainer-set direction, or there are 2 or more abandoned implementation attempts. | required |
| unclaimed | Assignees, linked PRs, and complete comment thread | Pass if nobody is currently assigned or actively working on the issue and there is no open PR. Old claims, closed PRs, and abandoned or expired claims do not count. | required |
| contribution-policy | Contribution policy in the repo-facts block | Pass unless the repo explicitly bans AI-assisted contributions. Conditions such as disclosure or testing are allowed. No stated policy also passes. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept only if every required check passes. Reject if any required check fails. Unclear counts as fail.
