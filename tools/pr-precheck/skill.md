
# PR Precheck — Submission Readiness

## Purpose

Evaluate exactly one pull request package and determine whether it is ready to submit. Compare the proposed changes against the issue, implementation plan, diff, pull request description, and test evidence.

The tool must not approve work based on confidence, formatting, or unsupported claims. Every check must cite specific evidence.

## Required Components

Read and apply:
- `rubric.md` for checks and the final verdict rule.
- `procedure.md` for the evaluation steps.
- `references/evidence-guide.md` for evidence locations.

Do not invent checks or procedures if these files are empty or incomplete. Refuse to grade if the rubric or procedure has no substantive content.

## Live Mode

Use live mode for a student's actual pull request before submission.

1. Read `scope.md` first.
2. Confirm the pull request belongs to the repository specified by `Repo:` in `scope.md`.
3. If the repository is unspecified or outside scope, stop without grading.
4. Read the issue, repository rules, PR template, and relevant discussion.
5. Read the implementation plan, including deviations, branch diff, commits, draft PR title and description, and test evidence.
6. Read `voice-guide.md` and identify any violations of the student's communication rules.
7. Follow `procedure.md` and apply every check in `rubric.md`.

Report voice-guide violations in the readable summary. Voice-guide findings affect the verdict only when a rubric check explicitly requires them.

## Eval Mode

Use eval mode when given a complete evaluation package.

- Evaluate exactly one package.
- Treat the package as the entire evidence universe.
- Do not fetch external information or inspect other repositories.
- Ignore `scope.md` and `voice-guide.md`.
- Apply every rubric check and the complete verdict rule.
- Never invent missing evidence.

## Evidence and Grading

Each check must receive one grade: `pass`, `fail`, or `unclear`.

Each check must include a one-line evidence statement naming the fact, quotation, or missing evidence that determined its grade.

Use `accept` only when the rubric's complete verdict rule permits it. Otherwise use `reject`.

There is no third verdict and no "accept with reservations."

## Output Format

A readable per-check summary may appear first. The response must end with one fenced JSON block, with nothing after it.

Use this exact structure and field order:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {
      "name": "<check name>",
      "grade": "pass|fail|unclear",
      "evidence": "<one line: the fact or quote that decided it>"
    }
  ],
  "verdict": "accept|reject"
}
```

Replace the placeholders with actual evidence and the final verdict. Do not add, remove, or reorder schema fields.
