# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the repository is not read.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57

**Verdict output**

All required checks pass, so the verdict is accept. On fit: this is a good match for you — the repro is handed to you, the fix is path-filtering logic in a single tool file, and node_modules/ and build/ are artifacts you already know from JS and React work, so no unfamiliar subsystem to learn. When you open the PR, the template requires all five CI jobs green, and the two named tests should go from failing to passing without disturbing the rest of tests/unit/test_tech_detector.py.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57",
  "checks": [
    {"name": "Maintainer activity", "grade": "pass", "evidence": "All 5 latest main commits human-authored by Aburke225; newest 2026-09-16T21:42:18Z, 12 days before the 2026-09-28 capture date (<180)."},
    {"name": "Repository in use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16T21:50:23Z, 12 days before capture (<365); no releases published."},
    {"name": "Newcomer-sized scope", "grade": "pass", "evidence": "One bounded change: \"tech_detector.py does not exclude node_modules/ or build/ paths\", with a repro snippet and two named failing tests (test_node_modules_excluded, test_build_directory_excluded); labeled 'good first issue', 'tier-1'."},
    {"name": "Issue availability", "grade": "pass", "evidence": "assignees: []; comments: 0; timeline shows no cross-referenced or linked PRs, and all 4 repo PRs reference other issues (#61, #72, #60, #68)."},
    {"name": "Contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI-generated/AI-assisted restriction; PR template and README state none either."}
  ],
  "verdict": "accept"
}

---

## Eval iterations

**Run history**

Run 1: agreement: 17/20 scored items (bar: 18/20: below the bar)

Run 2: agreement: 18/20 scored items (bar: 18/20: PASS)

**Issue analysis**

issue-19 — My rubric's decision was reject, while the gold label was accept. The evaluation output stated: "failed: Newcomer-sized scope." The issue described multiple potential causes and several implementation suggestions, so the Newcomer-sized scope check treated it as broader than one bounded contribution.

**Check rationale**

"Pass if the issue requests one bounded contribution and is not an umbrella/tracking issue, pure usage/support question, unresolved design discussion, or a change that a maintainer explicitly says requires core-internal or architectural work."

I kept this check because the purpose of the skill is to identify an appropriate first contribution. Requiring one bounded contribution helps prevent a newcomer from selecting an issue whose implementation scope is unclear, architectural, or substantially larger than it first appears.

**Trade-offs**

This check can be conservative. In the final evaluation, issue-19 had a gold label of accept, but my rubric rejected it because it failed the Newcomer-sized scope check. I accept this trade-off because I would rather reject a potentially manageable issue than recommend an issue whose scope may be too broad for a first contribution.

---

## Selection rationale

**Selection rationale**

1. Issue #57 fits my interests because it is a clearly scoped programming and debugging task. It gives me an opportunity to work within an existing codebase without requiring a major architectural change, and its tier-1/good-first-issue scope makes it realistic for the time available.

2. The verdict correctly identified that the repository is active, the issue is bounded, the contribution policy is acceptable, and there is no active implementation blocking the issue. Beyond the rubric, I also considered whether the task sounded understandable and useful for improving my debugging and codebase-navigation experience.

3. I anticipate that claiming the issue should be straightforward because the live evaluation found no assignee or active pull request implementing #57. I would still check the issue immediately before claiming it in Unit 2 in case another student begins working on it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/issue-select/`.
