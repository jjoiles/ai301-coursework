
# PR Precheck Rubric

## Purpose

Determine whether one pull request package is ready to submit by checking its issue alignment, implementation plan, code changes, test evidence, and PR description.

Grade every check using evidence from the package, not assumptions.

## Check 1: Issue Alignment

**Pass:** The PR identifies the issue it addresses, and the changes directly address the behavior or requirements stated in that issue.

**Fail:** The PR addresses a different issue, contradicts the issue requirements, or includes unrelated changes without justification.

**Unclear:** The issue or its requirements cannot be identified from the available evidence.

## Check 2: Plan and Diff Alignment

**Pass:** The diff implements the stated plan, or any deviations are explicitly documented with a reason. The changed files and behavior remain within the intended scope.

**Fail:** The diff contradicts the plan, introduces unexplained changes, or omits a required planned change without explanation.

**Unclear:** The plan, diff, or necessary deviation information is missing or insufficient to compare.

## Check 3: Reproduction and Test Evidence

**Pass:** The package includes concrete evidence of the original behavior and relevant verification after the change. Commands, test cases, and results are stated clearly enough to evaluate whether the fix works.

**Fail:** The evidence demonstrates that the fix does not work, relevant tests failed without resolution, or the PR falsely claims tests passed.

**Unclear:** Test evidence is absent, too vague to verify, or does not establish the claimed outcome.

## Check 4: PR Description Accuracy

**Pass:** The PR title and description accurately explain the change, its purpose, testing, and known limitations. Claims are consistent with the diff and evidence.

**Fail:** The description makes claims contradicted by the diff or test results, hides significant limitations, or promises functionality not implemented.

**Unclear:** The title or description is missing essential information needed to verify the submission.

## Check 5: Scope and Repository Standards

**Pass:** The change respects the applicable issue constraints and any repository standards explicitly included in the package. Unrelated modifications are absent or justified.

**Fail:** The change violates an explicitly stated repository requirement, or contains unrelated modifications that are not justified.

**Unclear:** A relevant required standard is identified but compliance cannot be verified.

Do not invent repository standards that are not provided in the evidence.

## Check 6: AI Use Disclosure

**Pass:** The PR description explicitly states whether AI assistance was used and, if used, describes its role without making unsupported claims.

**Fail:** The package contains evidence of AI assistance that the PR description falsely denies, or its disclosure contradicts other evidence.

**Unclear:** The PR description does not state whether AI assistance was used.

## Verdict Rule

Evaluate all six checks for every package.

- Return `accept` only when all six checks receive `pass`.
- Return `reject` when any check receives `fail` or `unclear`.
- Missing or unverifiable evidence must not be treated as passing.
- Never issue a conditional acceptance or a third verdict.

For each check, provide one evidence line quoting or identifying the exact package fact that determined the grade.

## Evidence Interpretation

Evaluate whether the supplied evidence establishes each check's passing condition, rather than requiring every possible form of supporting documentation. A documented, justified deviation or explicitly deferred behavior is not automatically a plan mismatch. Reproduction transcripts showing the corrected behavior, relevant passing tests, and a valid control case can establish sufficient test evidence without additional CI logs unless the repository explicitly requires them. A PR description may accurately identify limitations or deferred work without failing description accuracy. Do not mark a check unclear solely because the evidence uses a different presentation format when the supplied facts are sufficient to evaluate the requirement.

## Output

Use the JSON schema defined in `SKILL.md`.

The `checks` array must contain all six checks in the order listed above, using their exact names.

The final fenced JSON block must be the last content in the response.

## Evaluation checks

| Check | What to examine | Passing condition | Weight |
| --- | --- | --- | --- |
| Issue Alignment | Issue context and proposed changes | The PR addresses the reported issue without unrelated changes. | required |
| Plan and Diff Alignment | Accepted plan and actual code diff | The changes implement the plan without unexplained deviations. | required |
| Reproduction and Test Evidence | Before-and-after results and tests | Evidence demonstrates the fix and relevant tests passing. | required |
| PR Description Accuracy | PR title, description, and diff | The description accurately represents the implemented change and verification. | required |
| Scope and Repository Standards | Repository rules and PR template | The PR follows applicable contribution requirements and template sections. | required |
| AI Use Disclosure | Repository AI policy and PR disclosure | AI assistance is disclosed when required by repository policy. | required |

Verdict rule: Return `accept` only when all six required checks pass. Return `reject` if any check fails or is unclear.

## AI disclosure clarification

For the AI Use Disclosure check, apply the following rules:

- Pass when the repository explicitly requires AI-use disclosure and the PR provides the required disclosure.
- Pass when the repository does not require AI-use disclosure and the PR does not include one.
- Pass when the repository permits AI assistance and the PR accurately follows its stated disclosure policy.
- Fail when the repository explicitly requires disclosure and the PR omits or contradicts it.
- Fail when the repository explicitly prohibits AI-generated contributions and the PR violates that policy.
- Do not assume AI was used merely because the PR does not mention AI.
- Do not reject a PR solely because it lacks an AI disclosure when the repository does not require one.
- If the supplied repository facts are insufficient to determine whether an applicable disclosure requirement was violated, grade unclear rather than inventing a requirement.

This clarification applies to the AI Use Disclosure check wherever it appears in the rubric. It does not override an explicit repository policy.
