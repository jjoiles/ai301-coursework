
# Contribution: Fix Tech Detector Generated Directory Exclusions

**Contribution Number:** 1  
**Student:** Jean Joiles  
**GitHub Username:** jjoiles  
**Issue:** [Issue #57 (PathReview)](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57)  
**Pull Request:** [PR #85](https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85)

---

## Toolkit

Each story section below ends with a Toolkit block. These are the four tools supported by my earlier toolkit evaluation records (labeled Units 5–8 here; the linked repository evidence is under `beat-1-sandbox/unit-1` through `unit-4`). I have not verified separate Unit 9–12 artifacts. The tools are: issue-select, repro-check, plan-check, and pr-precheck. I do not claim work on other tools without evidence.

**Unit 5: issue-select, an issue-suitability rubric tested and refined (September 28–29, 2026)**

I built issue-select to judge a candidate issue on five criteria: maintainer activity, repository activity, newcomer-sized scope, issue availability, and contribution policy. Its first evaluation scored 17/20, and after refinement it scored 18/20 (PASS). The remaining disagreements were issue-15 (expected reject, tool accepted) and issue-19 (expected accept, tool rejected on scope). I kept the conservative scope requirement rather than loosening it to match the expected answer.

**Unit 6: repro-check, a reproduction-package check (October 5, 2026)**

repro-check judges whether a reproduction package has enough information to investigate and verify a reported issue. An early evaluation reached 12/17 scored agreements and hit three Windows encoding errors, and the evaluator was sometimes too strict about missing details. I revised the guidance to separate essential missing information from harmless omissions that an experienced developer can infer. The result was 18/20, then 19/20 (PASS) on October 5. The remaining disagreement was pkg-05, which the tool rejected for reproduction steps when acceptance was expected.

**Unit 7: plan-check, an implementation-plan check (October 12, 2026)**

plan-check evaluates whether a plan has an evidence-based diagnosis, bounded scope, actionable steps, observable tests, and an honest account of uncertainty. Its October 12 evaluation scored 19/20 (PASS). The one disagreement was pkg-14, which it rejected over concerns about diagnosis strength and treatment of risks. I kept the requirement that verified observations be distinguished from hypotheses rather than relaxing it.

**Unit 8: pr-precheck, a pull-request readiness rubric (October 20, 2026)**

pr-precheck reviews six areas: issue alignment, plan-and-diff alignment, reproduction and testing evidence, PR description accuracy, scope and repository standards, and AI-use disclosure. Earlier evaluations scored 14/19 and 18/20, with Windows encoding problems and inconsistent judgments about AI disclosure and overlapping criteria. I tied the disclosure check to documented repository policy and consolidated overlapping checks. The final result was 20/20 (PASS), with all five evaluated category groups passing.

---

## Why I Chose This Issue

I was assigned PathReview Issue #57, where generated and dependency files were being counted when the technology detector decided a project's primary programming language. The issue had a defined scope, and regression tests for the behavior already existed in the repository. It also gave me a chance to investigate Python path handling and to practice test-driven bug fixing. I documented my intent to work on it in a claim comment.

**Claim comment:** [Issue #57 claim comment](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-5999392681)

**Issue selection context:** Issue #57 was assigned to me rather than discovered through my own issue search. I developed and evaluated `issue-select` as part of the course, but I do not remember its verdict on Issue #57 and do not have evidence of a specific scan of that issue. I therefore cannot claim that the tool selected it for me. My decision to proceed was based on the specific and testable problem, the existing regression tests, and the opportunity to investigate Python path handling. The lack of a saved issue-specific scout verdict limits what I can report about that tool for this issue.

issue-select is not perfect. Its final evaluation was 18/20, and the remaining disagreements show that judging whether an issue is genuinely newcomer-sized is partly subjective. I treat its verdict as decision support, not a replacement for my own reading of the issue.

**Toolkit**

- Tool: `issue-select`. I developed and evaluated it as a suitability rubric; I cannot verify that I ran it on assigned Issue #57. It checks five criteria: maintainer activity, repository activity, newcomer-sized scope, issue availability, and contribution policy. Requiring all five guards against picking an abandoned, oversized, unavailable, or policy-blocked issue just because it carries a beginner-friendly label.
- What it produced: an 18/20 (PASS) evaluation on its test cases. The evaluation score is verified; the specific verdict on Issue #57 remains unverified.
- Difficulties: two remaining disagreements, issue-15 (expected reject, tool accepted) and issue-19 (expected accept, tool rejected on scope).
- What changed: the first evaluation scored 17/20, and refinement raised it to 18/20. I kept the conservative scope requirement rather than weakening it to match issue-19's expected answer.

---

## Understanding the Issue

**Problem Description**

Generated and dependency files were included when the detector identified a repository's primary programming language, so files in directories like `node_modules/` and `build/` could outweigh the project's own source.

**Expected Behavior**

Files under `node_modules/` and `build/` should be excluded, so the detector identifies Python as the primary language for the project in the reproduction case.

**Current Behavior**

Before the fix, the detector reported JavaScript.

**Affected Components**

- `agent/tools/tech_detector.py`, particularly `_should_skip_file()`
- `tests/unit/test_tech_detector.py`

The root cause was that exclusion checks such as `/node_modules/` did not match repository-relative paths that begin with `node_modules/`, because those paths have no leading slash.

**Toolkit**

- Tool: Direct source-code inspection and the existing `test_tech_detector.py` regression tests; no separate toolkit tool is verified for this phase.
- What it produced: Identified `_should_skip_file()` and its leading-slash exclusion-pattern mismatch as the cause of the observed language-detection error.
- Difficulties: Repository-relative paths did not match the original slash-prefixed exclusion patterns.
- What changed: The subsequent implementation plan specified normalized path components instead of substring matching.

---

## Reproduction Process

**Environment Setup**

- Development environment: GitHub Codespaces (confirmed from my recollection).
- Python version: 3.12 (confirmed from my recollection).
- Repository setup: I cloned the repository and installed dependencies in Codespaces.
- Dependency installation command (recorded in my [GitHub reproduction comment](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-6000149101)): `python -m pip install -e ".[dev]"`. I cloned the repository first, then ran the command from its root. The exact clone command is not preserved.
- Challenges and how I solved them: The issue-specific tests were marked `xfail`, so I ran them with `--runxfail` to see their actual failures. Both failed before the fix, confirming the problem. No separate Codespaces setup failure was documented.

**Steps to Reproduce**

1. Clone and open the PathReview repository in Codespaces, then install dependencies with `python -m pip install -e ".[dev]"`.

2. Run this command from the repository root:

    python -c "from agent.tools.tech_detector import TechDetector; t=TechDetector(); files=['main.py','core/app.py','node_modules/lib/util.js','node_modules/x/a.js','node_modules/y/b.js','build/bundle.js','build/vendor.js']; print(t.execute({'files': files}).data['primary_language'])"

3. Observed result before the fix: `JavaScript`, which is incorrect.

4. Result after the fix: `Python`, which is the expected result.

5. Run the two regression tests before the fix with:

    python -m pytest tests/unit/test_tech_detector.py -k "test_node_modules_excluded or test_build_directory_excluded" -v --runxfail

The [reproduction comment](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-6000149101) records `2 failed, 25 deselected in 0.35s` before implementation.

**Reproduction Evidence**

- **Commit showing reproduction:** No separate reproduction-only commit verified. [Fix commit `6a6c58f`](https://github.com/jjoiles/pathreview-ai301-fa26-howard/commit/6a6c58f) contains the implemented change; the [upstream reproduction comment](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-6000149101) records the before-fix evidence.
- **Reproduction comment:** [Reproduction evidence comment](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-6000149101)
- **Screenshots/logs:** The [Unit 7 plan-and-implement record](https://github.com/jjoiles/ai301-coursework/blob/main/beat-1-sandbox/unit-3/plan-and-implement.md) contains the before-and-after console output and pytest results. No screenshot is necessary for this backend-only fix.
- **My findings:** The two existing regression tests, `test_node_modules_excluded` and `test_build_directory_excluded`, both failed before the fix when run with `--runxfail`. That confirmed the bug independently of my one-line reproduction command.

**Toolkit**

- Tool: `repro-check`. I developed and evaluated this checker while documenting the reproduction. It checks whether a reproduction package contains the steps, environment, actual behavior, expected behavior, and repository-specific requirements needed to verify an issue.
- What it produced: a 19/20 (PASS) evaluation on its test cases.
- Difficulties: an early evaluation of 12/17 with three Windows encoding errors, and a tendency to be too strict about missing details. The remaining disagreement was pkg-05.
- What changed: I revised the guidance so essential missing information fails a package but minor details an experienced developer can infer do not.

---

## Solution Approach

**Analysis**

`_should_skip_file()` in `agent/tools/tech_detector.py` used substring checks such as `/node_modules/`. Paths in the file list are repository-relative, so a path like `node_modules/lib/util.js` does not start with a slash and the check never matched. Generated files were therefore counted toward the language totals.

**Proposed Solution**

Normalize path separators and check directory components instead of relying on substring matching. I am deliberately not changing existing exclusions or any unrelated language-detection behavior.

**Implementation Plan**

1. Modify `_should_skip_file()` in `agent/tools/tech_detector.py`.
2. Normalize path separators and evaluate directory components rather than using substring matching.
3. Preserve existing exclusions and avoid unrelated language-detection changes.
4. Enable the existing regression tests and verify the results.

The fix was developed on branch `fix/57-exclude-generated-files`, commit [`6a6c58f`](https://github.com/jjoiles/pathreview-ai301-fa26-howard/commit/6a6c58f).

**Implementation plan evidence:** [Implementation plan comment](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-6128465522)

**Deviations:** No departure from the posted plan is documented in the recovered implementation record. The existing regression tests were enabled by removing their `xfail` markers; no new regression tests were added.

**Toolkit**

- Tool: `plan-check`. I developed and evaluated it alongside my documented implementation plan. It evaluates whether a plan has an evidence-based diagnosis, bounded scope, actionable steps, observable tests, and an accurate account of uncertainty.
- What it produced: a 19/20 (PASS) evaluation on its test cases on October 12, 2026.
- Difficulties: it rejected pkg-14 (expected accept) over concerns about diagnosis strength and treatment of risks.
- What changed: I kept the requirement that verified observations be distinguished from hypotheses.

---

## Testing Strategy

The two regression tests, `test_node_modules_excluded` and `test_build_directory_excluded`, target this specific bug. Before the fix, both failed when run with `--runxfail`. After the fix, both pass. I also re-ran the reproduction command, which changed from `JavaScript` to `Python`.

The complete detector test suite checks that the change did not break other detector behavior:

    python -m pytest tests/unit/test_tech_detector.py -q
    27 passed in 0.24s

| Verification | Before | After |
| --- | --- | --- |
| Generated-directory regression tests | 2 failed | 2 passed |
| Primary-language detection | JavaScript | Python |
| Complete detector test suite | — | 27 passed |
| Pull request CI | — | 5 checks passed |

**Toolkit**

- Tool: pytest, run directly. It is not one of my toolkit tools.
- What it produced: 27 passed in 0.24s, plus the 2 regression tests flipping from failed to passed.
- Difficulties: none recorded.
- What changed: nothing.

---

## Implementation Notes

**September 28–29, 2026**

Initial issue-suitability tool evaluation; Issue #57 was assigned, not discovered by the tool. issue-select improved from 17/20 to 18/20 (PASS).

**October 5, 2026**

Reproduction documentation and test evidence. repro-check reached 19/20 (PASS) after earlier encoding problems.

**October 12, 2026**

Implementation plan, path-filtering fix, and successful tests. plan-check scored 19/20 (PASS). I did not write new regression tests. I enabled the two existing tests by removing their expected-failure (`xfail`) markers.

**October 20, 2026**

Pull request preparation, final pr-precheck evaluation (20/20, PASS), and submission of PR #85.

**Toolkit**

- Tool: plan-check, used to evaluate the implementation plan followed by the fix. No additional toolkit tool for the implementation log was verified.
- What it produced: the evaluated plan described above.
- Difficulties: see the Solution Approach block (pkg-14).
- What changed: nothing further recorded.

---

## Pull Request

**PR Link:** [PR #85](https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85)

**PR Description:** The [PR #85](https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85), titled "Fix tech detector generated directory exclusions for issue 57," explicitly says `Closes #57`, linking it to the issue in the same upstream repository. Its description summarizes the directory-exclusion bug, the fix, the two existing tests enabled by removing `xfail`, and the local `pytest tests/unit/test_tech_detector.py -v` result of 27 passing tests. It also reports five passing GitHub Actions checks and discloses AI assistance for development guidance, troubleshooting, and documentation.

**PR Evidence and Scope:** GitHub's [Files changed tab](https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85/files) shows exactly two changed files: `agent/tools/tech_detector.py` (path normalization and directory-component exclusion) and `tests/unit/test_tech_detector.py` (removal of the two `xfail` markers). No unrelated files were changed, and no new tests were added. The [Checks tab](https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85/checks) contains the CI results.

**Maintainer Feedback:**

- November 16, 2026: no maintainer feedback verified; PR #85 remained open.

**Status:** Awaiting review. The PR was open and awaiting maintainer review at last verification.

**Toolkit**

- Tool: `pr-precheck`. I developed and evaluated it during PR preparation, and checked the PR evidence against the same readiness criteria. It reviews issue alignment, plan-and-diff alignment, reproduction and testing evidence, PR description accuracy, scope and repository standards, and AI-use disclosure.
- What it produced: a final 20/20 (PASS) evaluation, with clear-accept 7/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, and unreviewable 3/3.
- Difficulties: the initial evaluation hit Windows encoding problems and rubric disagreements, including inconsistent judgments about AI-use disclosure and overlapping criteria. Earlier scores were 14/19 and 18/20.
- What changed: I tied the disclosure check to documented repository policy instead of assuming disclosure is universally required, and consolidated overlapping checks.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned that repository-relative paths behave differently from absolute paths when matching directory names: a check for `/node_modules/` cannot match a path that starts with `node_modules/`. Checking normalized directory components is more reliable than substring matching. I also practiced using existing `xfail` regression tests as a specification, enabling them and confirming they fail before the fix and pass after.

**Challenges Overcome**

The failing regression tests helped isolate the root cause: they failed for the generated-directory cases only, which pointed to the exclusion check in `_should_skip_file()` instead of the language-counting logic. On the tool side, Windows encoding errors and evaluation disagreements (issue-15, issue-19, pkg-05, pkg-14) pushed me to write more precise acceptance criteria.

**What I'd Do Differently Next Time**

The disagreements taught me that vague criteria, such as "newcomer-sized" or "essential" missing information, produce inconsistent verdicts, so I would define them more concretely from the start. I would also test the tools against real repository cases, such as ambiguous scopes, incomplete reproduction evidence, and PRs whose descriptions differ from their code, instead of relying only on my own test cases.

---

## Resources Used

- [PathReview Issue #57](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57)
- [Pull Request #85](https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85)
- [Unit 7 implementation documentation](https://github.com/jjoiles/ai301-coursework/blob/main/beat-1-sandbox/unit-3/plan-and-implement.md)
- [Unit 8 pull request documentation](https://github.com/jjoiles/ai301-coursework/blob/main/beat-1-sandbox/unit-4/pull-request.md)
- [Claim comment by jjoiles](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-5999392681)
- [Reproduction steps and dependency-installation command](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-6000149101)
- [PR code diff](https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85/files)
