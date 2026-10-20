# Unit 8 — Test and Submit

## Pull Request
https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85

## Issue
https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57

## Branch
fix/57-exclude-generated-files

## Summary
Fixed generated directory exclusions in the technology detector, including node_modules and build directories.

## Testing Evidence
- Both regression tests passed after the fix.
- All 27 technology detector tests passed locally.
- All five GitHub CI checks passed on PR #85.
- Official PR precheck evaluation: 20/20 (PASS).

## Reflection
This assignment reinforced the importance of matching implementation to the original issue, providing reproducible test evidence, and ensuring a pull request passes repository checks before submission.

## AI Assistance
AI assistance was used during development, documentation, and troubleshooting. Changes were verified through automated tests and the official evaluation harness.

## Run history

1. **Initial full evaluation:** 14/19 scored items agreed; one package (`pkg-05`) errored because Windows `cp1252` encoding could not handle characters in the prompt. The run was not saved as the official result.
2. **Encoding correction:** After enabling Python UTF-8, `pkg-05` ran but returned `reject` instead of the expected `accept` (0/1 agreement).
3. **Rubric revision:** I clarified the AI Use Disclosure check so it would not require disclosure when repository policy did not require it. The targeted evaluation of `pkg-01`, `pkg-02`, `pkg-05`, `pkg-08`, `pkg-13`, `pkg-16`, `pkg-19`, and `pkg-20` achieved **8/8 agreement**.
4. **Final full evaluation:** **20/20 agreement**, exceeding the required 18/20 threshold. All five categories passed. The official output was saved to `eval-run.txt`.
5. **Rubric consolidation:** I replaced the duplicated check definitions with one authoritative evaluation table to address instructor feedback. The first targeted run achieved 7/8 agreement. Further investigation identified `pkg-16` as a false rejection. After clarifying how sufficient evidence should be interpreted, a targeted rerun of `pkg-16` achieved 1/1 agreement. The final full evaluation achieved **18/20 (PASS)**, meeting the required threshold and all five category floors. The updated official results are recorded in `eval-run.txt`.

## Package analysis

- **pkg-02 (clear-accept):** Initially rejected due to PR Description Accuracy and AI Use Disclosure. After the clarification, it returned `accept`, matching the expected verdict.
- **pkg-05 (clear-accept):** Initially errored due to Windows encoding. After UTF-8 was enabled, it rejected on AI Use Disclosure. Following the rubric revision, it correctly returned `accept`.
- **pkg-08, pkg-13, pkg-16, and pkg-19 (clear-accept):** Initially rejected because AI disclosure was treated as mandatory even without an applicable repository requirement. The revised check accepted all four.
- **pkg-01 and pkg-20 (standards-wall):** Both continued returning `reject` after the revision, confirming that explicit repository standards were still enforced.
- **pkg-03 (silent-drift), pkg-04 (not-tested), and pkg-12 (unreviewable):** These were correctly rejected in the initial and final runs, providing regression evidence across other categories.

## Check rationale

I focused on **AI Use Disclosure** because it caused most of the incorrect clear-accept verdicts.

The check should compare a pull request against the repository's actual AI-use policy rather than assume every repository requires disclosure. Passing evidence includes a PR that follows the applicable policy, including disclosure when required. Failing evidence includes an omitted required disclosure or a violation of an explicit prohibition.

The check must not infer AI use solely because a disclosure statement is absent. This makes the decision evidence-based and avoids rejecting otherwise valid pull requests.

## Trade-offs

Making AI disclosure conditional on repository policy reduces false rejections, but it requires the reviewer to examine repository instructions carefully.

When policy evidence is insufficient, the tool should avoid inventing requirements and report uncertainty where appropriate.

The change could weaken enforcement of explicit repository standards, so I reran `pkg-01` and `pkg-20` as **standards-wall canaries**. Both remained correctly rejected.

The final 20-package evaluation achieved 18/20 agreement and passed all five category floors. A remaining limitation is that the tool depends on the repository evidence provided and cannot independently prove undisclosed AI use.