# Unit 8 — Test and Submit

## Pull Request
https://github.com/codepath/pathreview-ai301-fa26-howard/pull/85

## Issue
https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57

## Branch
fix/57-exclude-generated-files

## Summary
Fixed generated directory exclusions in the technology detector, including `node_modules` and `build` directories.

## Testing Evidence
- Both existing regression tests passed after removing their expected-failure (`xfail`) markers.
- All 27 technology detector tests passed locally.
- All five GitHub CI checks passed on PR #85.
- Official PR precheck evaluation: **18/20 (PASS)**, with `pkg-11` and `pkg-16` disagreeing with the expected verdicts. The committed `eval-run.txt` is the authoritative record.

## Reflection
This assignment reinforced the importance of matching implementation to the original issue, providing reproducible test evidence, and ensuring that a pull request passes repository checks before submission.

## AI Assistance
AI assistance was used during development, documentation, and troubleshooting. Changes were verified through automated tests and the official evaluation harness.

## Run history

1. **Initial full evaluation:** 14/19 scored items agreed; one package (`pkg-05`) errored because Windows `cp1252` encoding could not handle characters in the prompt. This was not saved as the official result.
2. **Encoding correction:** After enabling Python UTF-8, `pkg-05` ran but returned `reject` instead of the expected `accept` (0/1 agreement).
3. **Rubric revision:** I clarified the AI Use Disclosure check so it would not require disclosure when repository policy did not require it. The targeted evaluation of `pkg-01`, `pkg-02`, `pkg-05`, `pkg-08`, `pkg-13`, `pkg-16`, `pkg-19`, and `pkg-20` achieved **8/8 agreement**.
4. **Earlier full evaluation:** **20/20 agreement**, exceeding the required 18/20 threshold. All five categories passed. This earlier result was superseded by the final committed evaluation.
5. **Rubric consolidation:** I replaced duplicated check definitions with one authoritative evaluation table. The first targeted run achieved 7/8 agreement. A subsequent targeted rerun of `pkg-16` achieved 1/1 agreement. However, the final full evaluation achieved **18/20 (PASS)**, with `pkg-11` and `pkg-16` disagreeing with the expected verdicts. All five category floors passed. The authoritative results are recorded in `eval-run.txt`.

## Package analysis

- **pkg-02 (clear-accept):** Initially rejected due to PR Description Accuracy and AI Use Disclosure. After the clarification, it returned `accept`, matching the expected verdict.
- **pkg-05 (clear-accept):** Initially errored due to Windows encoding. After UTF-8 was enabled, it rejected on AI Use Disclosure. Following the rubric revision, it returned `accept`.
- **pkg-08, pkg-13, and pkg-19 (clear-accept):** Earlier targeted runs showed improved agreement after the AI Use Disclosure revision.
- **pkg-16 (clear-accept):** A targeted rerun returned `accept`, but the final committed evaluation returned `reject` against the expected `accept` verdict. This remains an unresolved disagreement.
- **pkg-11:** The final committed evaluation disagreed with the expected verdict. Together with `pkg-16`, this accounts for the two disagreements in the final 18/20 result.
- **pkg-01 and pkg-20 (standards-wall):** Both continued returning `reject` after the revision, confirming that explicit repository standards were still enforced.
- **pkg-03 (silent-drift), pkg-04 (not-tested), and pkg-12 (unreviewable):** These were correctly rejected in the initial and final runs, providing regression evidence across other categories.

## Check rationale

I focused on **AI Use Disclosure** because it caused several incorrect clear-accept verdicts.

The current rubric's AI Use Disclosure row is the authoritative definition of the check. The revision evaluates a pull request against documented repository AI-use requirements rather than assuming that disclosure is universally required.

This reduces false rejections while preserving enforcement of explicit repository policies. The absence of a disclosure statement alone does not establish that a policy was violated.

## Trade-offs

Making AI disclosure conditional on repository policy reduces false rejections, but it requires the reviewer to examine repository instructions carefully.

When policy evidence is insufficient, the tool should avoid inventing requirements and report uncertainty where appropriate.

The change could weaken enforcement of explicit repository standards, so I reran `pkg-01` and `pkg-20` as **standards-wall canaries**. Both remained correctly rejected.

A remaining limitation is that when a repository has no explicit AI-use disclosure policy, the tool may accept a PR that involved undisclosed AI assistance. This is an intentional trade-off: the check evaluates documented requirements rather than imposing an unsupported universal disclosure rule.The final 20-package evaluation achieved 18/20 agreement and passed all five category floors. A remaining limitation is that the tool depends on the repository evidence provided and cannot independently prove undisclosed AI use.
