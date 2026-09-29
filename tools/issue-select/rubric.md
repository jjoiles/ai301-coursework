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
   - Pass condition:Pass if the issue has one clearly defined outcome or problem to solve, even if completing it requires multiple related implementation or documentation changes. Fail only if it is an umbrella/tracking issue, a pure usage/support question, an unresolved design discussion with no actionable outcome, or the evidence explicitly indicates that the work requires broad architectural/core-internal changes unsuitable for a first contribution.
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
| Maintainer activity | Repo facts: last 5 default-branch commits and maintainer first-response sample; issue Comments author_association | Pass if at least one of the last 5 default-branch commits is human-authored within 180 days of the capture date OR the maintainer first-response sample shows at least one Owner, Member, or Collaborator response within 30 days. | required |
| Repository in use | Repo facts: archived flag, latest release, and last push to any branch | Pass if the repository is not archived AND either its latest release or last push occurred within 365 days of the capture date. | required |
| Newcomer-sized scope | Issue body and Comments section | Pass if the issue requests one bounded contribution and is not an umbrella/tracking issue, pure usage/support question, unresolved design discussion, or a change that a maintainer explicitly says requires core-internal or architectural work. | required |
| Issue availability | Repo facts: this issue assignees and linked PRs; Comments section for claim comments and PR mentions | Pass if there is no assignee and no open linked or comment-mentioned PR actively implementing the issue. Closed unmerged PRs count as abandoned attempts and do not fail this check. | required |
| Contribution policy | Repo facts: contribution policy, including CONTRIBUTING.md or dedicated AI policy files when provided | Pass if the repository does not explicitly ban AI-generated or AI-assisted contributions. Conditional policies requiring disclosure, testing, understanding, or human review pass; no stated AI policy also passes. | required |

## Verdict rule

Accept an issue only if all required checks pass. Reject the issue if any required check fails. If the available evidence is insufficient to determine whether a required check passes, treat that check as unclear and reject the issue.
