# Procedure: how this skill grades a plan package

## Read order

1. Read `scope.md` first to confirm that the issue and repository are within the skill's permitted scope. If the target is outside scope, stop and report the scope problem rather than grading an unrelated issue.

2. Read `rubric.md` and `references/evidence-guide.md` before examining the candidate. Record each required check, its pass condition, and the evidence locations needed to grade it. Use the rubric as the authority for decisions and the evidence guide as the map for locating proof.

3. Read the issue context and any available thread highlights. Record the reported problem, expected behavior, relevant constraints, maintainer instructions, and any existing discussion that could affect the proposed change.

4. Read the reproduction evidence before reading the candidate plan. Record the environment, triggering inputs, reproduction steps, actual results, expected results, and any limitations. This prevents the candidate plan's diagnosis from influencing what the evidence actually demonstrates.

5. Read the repository-facts block. Record relevant source files, architecture, setup instructions, tests, contribution conventions, templates, and any stated AI-assistance disclosure requirements. Do not assume a convention exists unless the supplied evidence establishes it.

6. Read the candidate plan and proposed plan comment. Record the stated diagnosis, scope boundaries, target files, implementation steps, test strategy, assumptions, risks, unknowns, and communication commitments.

7. In live mode, gather the equivalent information from the GitHub issue, posted reproduction comment, repository documentation, relevant source files, and local draft plan and comment. Compare these sources before assigning grades.

8. Grade only after the issue, reproduction, repository facts, plan, and proposed comment have been reviewed. Do not substitute assumptions or external facts for missing package evidence.

## Evidence gathering

1. **Diagnosis and grounding:** Compare the plan's stated cause with the issue context and reproduction evidence. Record the exact observed behavior, the claimed explanation, supporting facts, contradictions, and any proposed verification of uncertain causes.

2. **Scope:** Extract the plan's intended changes, excluded work, named files or components, and expected outcome. Compare these with the issue's requested behavior and repository facts. Record any unrelated features, refactoring, or unexplained expansion.

3. **Cause-directed approach:** Compare the proposed implementation with the reproduced failure and the relevant code path. Record whether the change addresses a plausible cause, merely hides the symptom, or includes a concrete investigation step before choosing between possible causes.

4. **Executability:** Extract the ordered implementation actions, starting files or components, prerequisites, required inputs, and decisions. Compare them with the repository's documented structure. Record any essential missing step that would prevent a contributor from beginning or continuing.

5. **Test plan:** Extract the proposed commands, tests, inputs, expected outputs, and success criteria. Compare them with the reproduction steps and observed failure. Record whether the checks exercise the relevant code path and can distinguish faulty behavior from corrected behavior.

6. **Honesty:** Identify factual claims, hypotheses, assumptions, risks, unknowns, and dependencies. Compare them with the issue, reproduction evidence, and repository facts. Record any material unsupported certainty or unresolved blocker, along with the plan's method for addressing it.

7. **Comms:** Compare the proposed plan comment with the issue thread, maintainer instructions, contribution documentation, templates, and stated disclosure policies. Record whether the comment identifies the specific issue, describes the bounded intended work, follows relevant instructions, and includes any required disclosure.

8. For every evidence item, retain its source location and a concise supporting quotation or factual description. Use the evidence guide to locate missing information before assigning a grade. Do not invent evidence.

## Check execution

1. Evaluate the rubric checks in their listed order: Diagnosis grounded in evidence, Bounded change, Cause-directed approach, Executable implementation steps, Observable test strategy, Honest uncertainties and risks, and Thread and repository conventions.

2. For each check, compare the gathered evidence directly against that check's stated pass condition. Judge whether the proposed work meets the outcome described by the condition, not whether the plan uses a particular format, number of headings, or writing style.

3. Assign `pass` when the available evidence establishes the pass condition. Assign `fail` when evidence establishes that the condition is violated. Assign `unclear` when essential evidence is missing, ambiguous, or insufficient to decide.

4. Before assigning `unclear`, consult the evidence guide and check all specified locations for that evidence. In live mode, inspect the corresponding available repository documentation, issue thread, and local drafts. Do not assume an unmentioned fact is true.

5. Do not fail a plan for minor details reasonably discoverable in the repository when the implementation remains executable. Do fail when an essential input, starting point, decision, or observable success condition is absent.

6. Treat hypotheses as acceptable when clearly identified and paired with an appropriate verification step. Do not require a confirmed root cause before investigation when the evidence does not establish one.

7. For communication conventions, apply only requirements actually established by the issue thread or repository. An explicitly required AI-assistance disclosure must be checked; if no such requirement is stated, do not invent one.

8. Record a separate grade and evidence explanation for every check. Once the relevant evidence has been gathered, grade from those recorded facts rather than repeatedly reinterpreting the entire package. Revisit a source only to resolve a specific contradiction or missing fact.

## Verdict assembly

1. Collect every check's name, grade, and evidence explanation in the same order as `rubric.md`.

2. Apply the rubric's binary verdict rule: `accept` only when every required check passes. Return `reject` when any required check fails or is unclear. Preferred checks, if added later, never change the verdict.

3. Treat `unclear` as a blocking result for required checks, but preserve the grade `unclear` in the check output rather than falsely describing missing evidence as a demonstrated failure.

4. For each failed or unclear required check, identify the decisive evidence or missing evidence and explain the smallest substantive correction needed. Quote the relevant source text when available. Do not recommend unrelated improvements as conditions for acceptance.

5. Produce the result in the JSON structure required by `SKILL.md`, preserving the exact rubric check names and the binary `accept` or `reject` verdict. Do not add unsupported claims or invent evidence.

6. If every required check passes, return `accept` even if minor stylistic or formatting improvements remain. If any required check is unresolved, return `reject` and identify the blocking check.

7. Ensure the final verdict agrees with the individual grades and can be reproduced by another executor applying the same rubric to the same evidence.
