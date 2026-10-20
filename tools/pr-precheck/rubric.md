# PR Precheck Rubric

## Purpose

Determine whether one pull request package is ready to submit by checking its issue alignment, implementation plan, code changes, test evidence, PR description, and applicable repository standards.

Evaluate each check using evidence supplied in the package. Do not invent facts, requirements, or repository policies.

## Evaluation Checks

The following table is the **single authoritative definition** of the six required checks. Apply each check's pass, fail, and unclear criteria.

| **Check** | **What to examine** | **Passing condition** | **Weight** |
| --- | --- | --- | --- |
| Issue Alignment | Issue statement, requirements, PR description, and diff | **Pass:** The PR identifies the issue and directly addresses its requirements without unjustified unrelated changes. **Fail:** The change addresses a different issue, contradicts its requirements, or introduces unjustified unrelated work. **Unclear:** The issue or its requirements cannot be identified from the evidence. | required |
| Plan and Diff Alignment | Accepted implementation plan, code diff, and documented deviations | **Pass:** The diff implements the plan, and any deviations are documented and justified. A documented, justified deviation or explicitly deferred behavior is not automatically a mismatch when it remains consistent with the accepted scope. **Fail:** The diff contradicts the plan, introduces unexplained changes, or omits required work without explanation. **Unclear:** The plan, diff, or deviation evidence is insufficient for comparison. | required |
| Reproduction and Test Evidence | Reproduction steps, before-and-after results, commands, and test output | **Pass:** Concrete evidence demonstrates the original problem and verifies the change through relevant tests. Reproduction transcripts showing corrected behavior, relevant passing tests, and a valid control case can establish sufficient evidence without additional CI logs unless repository requirements explicitly demand them. Judge the substance of verifiable evidence, not its presentation format. **Fail:** Tests demonstrate an unresolved failure, the fix does not work, or the PR falsely claims tests passed. **Unclear:** Evidence is missing, unverifiable, or insufficient to establish the outcome. | required |
| PR Description Accuracy | PR title, description, diff, testing claims, and limitations | **Pass:** The description accurately represents the implemented change, testing, and known limitations. Accurately disclosed limitations or explicitly deferred work do not constitute an accuracy failure when the description does not claim that work was completed. **Fail:** Claims contradict the diff or results, significant limitations are concealed, or unimplemented behavior is promised. **Unclear:** Essential information is missing or the supplied facts cannot establish accuracy. Do not mark a check unclear solely because sufficient evidence is presented in a different format. | required |
| Scope and Repository Standards | Issue constraints, contribution rules, repository instructions, PR template, and changed files | **Pass:** The PR complies with applicable documented standards and remains within justified scope. **Fail:** The PR violates an explicit repository requirement or includes unjustified unrelated changes. **Unclear:** An applicable requirement is identified but compliance cannot be established. Do not invent standards absent from the evidence. | required |
| AI Use Disclosure | Repository AI-use policy, PR disclosure, and supplied evidence of AI assistance | **Pass:** The PR follows the repository's applicable AI-use and disclosure requirements. When disclosure is required, the PR provides it accurately. When no disclosure requirement applies, absence of disclosure alone is not a failure. **Fail:** The PR omits or contradicts an explicitly required disclosure, falsely denies evidenced AI assistance, or violates an explicit AI-use prohibition. **Unclear:** An applicable policy or potential violation is identified but the supplied evidence cannot establish compliance. Do not infer AI use merely from a missing disclosure or invent a repository policy. | required |

## Verdict Rule

Evaluate all six required checks for every package.

- Return `accept` only when all six checks pass.
- Return `reject` if any required check fails or is unclear.
- Missing or unverifiable evidence must not be treated as passing when needed to establish compliance.
- Never issue a conditional acceptance or a third verdict.

For each check, provide one evidence line quoting or identifying the specific package fact supporting the grade.

## Output

Use the JSON schema defined in `SKILL.md`.

The `checks` array must contain all six checks in the order listed in the table, using their exact names.

The final fenced JSON block must be the last content in the response.
The final fenced JSON block must be the last content in the response.
