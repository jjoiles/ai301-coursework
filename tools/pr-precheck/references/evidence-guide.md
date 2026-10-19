
# PR Precheck Evidence Guide

## Purpose

This guide identifies where to find evidence when evaluating one pull request package. Use it with `rubric.md` and `procedure.md`.

Every check must cite a specific fact, quotation, command, result, or missing item. Do not infer evidence that is not present.

## 1. Issue Evidence

Look for:
- Issue number, title, and description.
- Expected behavior and reported problem.
- Acceptance criteria and constraints.
- Maintainer comments clarifying the issue.

Use this evidence for **Issue Alignment**.

A PR must address the issue's actual requirements, not simply mention its number.

## 2. Implementation Plan Evidence

Look for:
- The implementation plan (`plan.md`).
- Planned files and intended behavior changes.
- Known constraints and excluded work.
- Documented deviations and explanations.

Use this evidence for **Plan and Diff Alignment**.

Compare the planned work with the actual changes. Do not treat an unexplained deviation as automatically acceptable.

## 3. Diff and Commit Evidence

Look for:
- Changed file paths.
- Added, modified, or removed code.
- Commit messages and their relationship to the issue.
- Changes unrelated to the planned fix.

Use this evidence for **Plan and Diff Alignment**, **Issue Alignment**, and **Scope and Repository Standards**.

The diff is stronger evidence of what was implemented than a claim in the PR description.

## 4. Reproduction and Test Evidence

Look for:
- Original reproduction steps.
- Commands and environment information.
- Observed behavior before the change.
- Tests added or modified.
- Commands and results after the change.
- Failed tests, unresolved errors, and limitations.

Use this evidence for **Reproduction and Test Evidence**.

A statement such as "all tests pass" without supporting details is not sufficient by itself. Do not report tests as passing unless the supplied evidence supports that result.

## 5. PR Title and Description Evidence

Look for:
- The PR title and summary.
- The issue reference.
- Explanation of the change.
- Before-and-after behavior.
- Testing details.
- Known limitations.
- AI assistance disclosure.

Use this evidence for **PR Description Accuracy** and **AI Use Disclosure**.

Compare claims with the diff, plan, and test results. A polished description does not override contradictory evidence.

## 6. Repository Standards Evidence

In live mode, inspect:
- The repository's PR template.
- Contributor instructions.
- Explicit maintainer policies.
- Relevant issue discussion.

In eval mode, use only standards included in the package.

Use this evidence for **Scope and Repository Standards**.

Do not invent requirements that the repository or evaluation package does not state.

## 7. Missing or Conflicting Evidence

If evidence is missing, record what is missing and assign `unclear` where the rubric requires it.

If evidence directly contradicts a required condition, assign `fail`.

Do not fill gaps using assumptions, outside information in eval mode, or unsupported claims.

## 8. Evidence Reporting

For each check, record one concise evidence line.

Good example:
"Plan lists changes to the path filter, but the diff also modifies unrelated UI files without a deviation note."

Bad example:
"The PR looks incomplete."

The evidence must explain why the assigned grade follows the written rubric.

## Mode Restrictions

**Live mode:** Read the scoped repository, issue, plan, PR, diff, test evidence, and communication rules.

**Eval mode:** Read only the supplied package. Do not follow external links, inspect other files, or use information from other packages.
