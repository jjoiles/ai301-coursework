# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:** In an eval package, examine the issue context, reproduction-evidence block, candidate plan's stated diagnosis, and proposed implementation approach. Compare the claimed cause with the actual commands, inputs, outputs, errors, and behavior recorded in the reproduction evidence. In live mode, examine the GitHub issue description, the student's posted reproduction comment, the relevant source code, and the draft plan.

**What good looks like:** The diagnosis explains the behavior demonstrated by the reproduction evidence without contradicting it or claiming that an unverified root cause is certain. When the cause is unknown, the plan identifies a plausible explanation and a concrete investigation step to confirm it before implementation. The proposed change targets that cause rather than merely suppressing the visible failure.

## Scope

**Where it lives:** In an eval package, examine the candidate plan's scope statement, intended changes, excluded work, named files or components, and the issue context. Compare these against the repository-facts block to identify unrelated changes. In live mode, examine the draft plan, GitHub issue, relevant source files, and repository contribution guidance.

**What good looks like:** The proposed work is a coherent, bounded change addressing the reported issue. Supporting tests and necessary related edits are acceptable, but unrelated refactoring, new features, or changes to behavior outside the issue are not. The plan makes its intended boundaries understandable.

## Executability

**Where it lives:** In an eval package, examine the candidate plan's implementation approach, ordered steps, target files or components, prerequisites, and repository facts. In live mode, compare the draft plan against the repository's source tree, setup documentation, and the student's reproduction environment.

**What good looks like:** Another contributor familiar with the repository can identify the starting point, relevant code paths, intended modifications, and sequence of work without asking the author to make essential missing decisions. Small details that can reasonably be discovered while following the plan do not make it unexecutable.

## Test plan

**Where it lives:** In an eval package, compare the candidate plan's testing and verification steps with the reproduction-evidence block, issue's expected behavior, and repository-facts block. Look for specific commands, test targets, inputs, expected outputs, or observable behavior. In live mode, inspect the posted reproduction comment, existing tests, and draft verification plan.

**What good looks like:** The proposed checks exercise the relevant implementation path and distinguish the reported failure from the desired behavior. A before-and-after reproduction, an existing regression test, or another concrete observable check is sufficient when its expected result is clear. Generic statements such as "run tests" without an issue-relevant observable result are insufficient.

## Honesty

**Where it lives:** In an eval package, examine the plan's diagnosis, assumptions, risks, unknowns, dependencies, and any deviation notes against the reproduction evidence and repository facts. In live mode, examine the draft plan, actual investigation findings, implementation progress, and any updates to the GitHub issue thread.

**What good looks like:** The plan separates confirmed observations from hypotheses, acknowledges material unknowns, and provides a way to resolve uncertainties that affect implementation. An honest mid-build deviation explains what changed, why, and whether the original scope or posted intent was affected. If no deviation occurred, an explicit explanation is sufficient. Do not require invented risks or unnecessary speculation.

## Comms

**Where it lives:** In an eval package, compare the proposed plan comment with the issue context, thread highlights, repository-facts block, contribution instructions, templates, and any AI-assistance disclosure policy. In live mode, examine the actual GitHub issue discussion, maintainer comments, repository documentation, applicable contribution policies, and the student's draft plan comment.

**What good looks like:** The comment identifies the specific issue, explains the bounded intended change, and reflects relevant maintainer instructions or previous discussion. It does not promise an unsupported outcome or deadline, misrepresent completed work, or ignore required contribution conventions. Where a repository explicitly requires AI-assistance disclosure, the comment follows that requirement. Do not invent disclosure obligations when none are stated.
