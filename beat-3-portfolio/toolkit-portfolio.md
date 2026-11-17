**Student:** Jean Joiles

## Featured Tools

I chose three tools that cover three stages of an open-source contribution: deciding whether an issue is worth taking (issue-select), determining whether its reported problem can be reproduced (repro-check), and verifying that a pull request is ready for review (pr-precheck). Each has recorded evaluations, so each shows how the tool was tested and refined, and all three moved measurably through use.

**issue-select**

**What it is, and the judgment hole I wrote:** issue-select assesses a candidate issue against five criteria: maintainer activity, repository activity, newcomer-sized scope, issue availability, and contribution policy. The judgment is the requirement that all five hold. A beginner-friendly label alone shouldn't lead me to an abandoned, oversized, already-claimed, or policy-blocked issue.

**How it evolved, dated:**

- September 28–29, 2026: The first evaluation scored 17/20, with disagreements over what counts as newcomer-sized work. After refinement, the later evaluation scored 18/20 (PASS), with two remaining disagreements. issue-15 was expected to be rejected but the tool accepted it. issue-19 was expected to be accepted but the tool rejected it on scope. I kept the conservative scope requirement rather than loosening the threshold just to match the expected answer for issue-19.

**Evidence:**

- Run 1: 17/20. Run 2: 18/20, PASS.
- issue-15: expected reject, verdict accept.
- issue-19: expected accept, verdict reject, reason: newcomer-sized scope.
- Category results: claimed 4/4, clear-accept 7/8, dead-repo 3/3, policy 1/1, scope 3/4.
- Source: [Unit 1 — issue-select evaluation](https://github.com/jjoiles/ai301-coursework/blob/main/beat-1-sandbox/unit-1/eval-run.txt)

**repro-check**

**What it is, and the judgment hole I wrote:** repro-check assesses whether a reproduction package has enough information to investigate and verify a reported issue: the steps followed, environment, actual behavior, expected behavior, and repository-specific requirements. The judgment is that essential instructions must be explicit, but minor details an experienced developer can reasonably infer shouldn't make an otherwise reproducible report fail.

**How it evolved, dated:**

- October 2026: An early evaluation reached only 12/17 scored agreements and hit three Windows encoding errors. The evaluator was also sometimes too strict about missing details. I revised the guidance to separate essential missing information from harmless omissions. An intermediate run scored 18/20 (PASS), and the final October 5 run scored 19/20 (PASS).

**Evidence:**

- Earlier: 12/17. Intermediate: 18/20, PASS. Final: 19/20, PASS.
- The remaining disagreement is pkg-05: expected accept, verdict reject, reason: reproduction steps.
- Final category results: clear-accept 7/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4.
- Source: [Unit 2 — repro-check evaluation](https://github.com/jjoiles/ai301-coursework/blob/main/beat-1-sandbox/unit-2/eval-run.txt)

**pr-precheck**

**What it is, and the judgment hole I wrote:** pr-precheck is a rubric with six areas: issue alignment, implementation-plan and code-diff alignment, reproduction and testing evidence, PR description accuracy, scope and repository standards, and AI-use disclosure. The judgment is that a PR shouldn't pass just because its code looks plausible. The changes must match the reported problem, be adequately tested, and be described accurately to reviewers. AI disclosure is judged against the repository's actual documented policy, not assumed to be universally required.

**How it evolved, dated:**

- October 20, 2026: An earlier evaluation hit Windows character-encoding problems and inconsistent judgments. I revised the guidance to distinguish a real policy violation from an assumption about AI disclosure, and consolidated overlapping checks so decisions were more consistent. Agreement rose from 14/19 and 18/20 in earlier runs to 20/20 in the final committed result.

**Evidence:**

- Earlier: 14/19. Targeted: 8/8. Subsequent: 18/20. Final: 20/20, PASS.
- Final category results: clear-accept 7/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, unreviewable 3/3.
- Source: [Unit 4 — pr-precheck evaluation](https://github.com/jjoiles/ai301-coursework/blob/main/beat-1-sandbox/unit-4/eval-run.txt)
- Real contribution, PathReview Issue #57 (PR #85, open): the technology detector was counting generated and dependency files in `node_modules/` and `build/`, so a project's primary language read as JavaScript. After the fix (commit 6a6c58f, branch `fix/57-exclude-generated-files`), it reads Python. Local detector tests passed 27/27 and 5/5 reported CI checks passed. The PR description states that existing regression tests were enabled rather than claiming new tests were written. This is the kind of scope, testing-evidence, and description-accuracy review pr-precheck is built to enforce.

## Inventory

- **plan-check:** Evaluates whether an implementation plan has an evidence-based diagnosis, bounded scope, actionable steps, observable tests, and an accurate account of uncertainty. Its October 12, 2026 evaluation scored 19/20 and passed. The one disagreement was pkg-14, which it rejected over concerns about diagnosis strength and treatment of risks. Source: [Unit 3 — plan-check evaluation](https://github.com/jjoiles/ai301-coursework/blob/main/beat-1-sandbox/unit-3/eval-run.txt)
- **issue-scout:** Intended to search for suitable contribution opportunities. Installation, execution, and search-strategy revisions are not documented in this portfolio, so I don't present it as a tested tool.
- **voice-guard:** Intended to assess writing or communication style. Installation and testing are not documented in this portfolio.
- **ship-gate:** Intended to check readiness before submitting a PR. Installation and testing are not documented in this portfolio.
- **PR monitor:** Intended to track pull request status and later activity. Installation and execution are not documented in this portfolio.

## The Arc

**Beat 1**

Date: September 28–29, 2026

Friction: The issue-selection rubric first scored 17/20, with disagreements including how newcomer-sized work was classified.

Change: I refined the evaluation guidance while keeping the requirement that a suitable issue must meet the scope criterion.

Result: 18/20 scored agreements; PASS.

**Beat 2**

Date: October 2026

Friction: The reproduction evaluator produced Windows encoding errors and was sometimes too strict about missing details.

Change: I made the guidance distinguish necessary steps from minor information that could reasonably be inferred.

Result: 19/20 scored agreements; PASS.

**Beat 3**

Date: October 12, 2026

Friction: plan-check rejected pkg-14 even though its expected classification was acceptance, because of concerns about diagnosis confidence and how uncertainty was handled.

Change: I kept the conservative requirement that verified observations be distinguished from hypotheses.

Result: 19/20 scored agreements; PASS.

**Beat 4**

Date: October 20, 2026

Friction: pr-precheck hit encoding issues and gave inconsistent judgments around AI-use disclosure and overlapping review criteria.

Change: I tied disclosure requirements to documented repository policy and consolidated the overlapping guidance.

Result: 20/20 scored agreements; PASS, with all five evaluated category groups passing.

## Limitations and What's Next

My evaluation scores measure agreement with the test cases I supplied. They don't show that a tool will correctly read every real repository, a contribution policy that changes, an ambiguous issue, or a development action no one reported. These tools are structured decision support, not a replacement for human review. Testing for several of my other tools (issue-scout, voice-guard, ship-gate, PR monitor) is not documented in this portfolio, so the toolkit's evidence is strongest for the first stages of the contribution workflow. Next, I would expand the evaluation cases with real repository examples: ambiguous scopes, incomplete reproduction evidence, evolving policies, and PRs whose descriptions differ from their actual code changes. I would also bring the remaining tools up to the same standard of recorded evaluation.

**Tool limits.**

issue-select: The two remaining disagreements (issue-15 accepted when it should have been rejected, issue-19 rejected when it should have been accepted) show that judging whether an issue is genuinely newcomer-sized can be subjective.

repro-check: The remaining pkg-05 disagreement shows that deciding whether missing reproduction details are essential or inferable is not always straightforward.

pr-precheck: It depends on the evidence submitted and on the repository's documentation, and it cannot independently prove whether AI assistance was used but not disclosed.
