
# PR Precheck Procedure

## Purpose

Evaluate exactly one pull request package to determine whether it is ready to submit.

Follow the checks in `rubric.md` without inventing additional requirements. Every decision must be supported by evidence.

## Step 1: Determine the Evaluation Mode

Identify whether the input is a live pull request or an evaluation package.

### Live Mode

1. Read `scope.md` before inspecting any other input.
2. Confirm that the `Repo:` field identifies the section's Path Review repository.
3. If `Repo:` is missing, contains a placeholder, or does not identify a repository, stop without grading and request a completed scope.
4. Confirm that the PR belongs to the scoped repository. Refuse to grade an out-of-scope PR.
5. Read `voice-guide.md` for the student's communication rules.
6. Gather the issue, discussion, PR template, repository policies, implementation plan, deviations, commits, diff, PR title and description, and test evidence.

### Eval Mode

1. Use only the supplied evaluation package.
2. Do not access external repositories, links, files, or other packages.
3. Ignore `scope.md` and `voice-guide.md`.
4. Treat absent evidence as absent, even when the package contains links suggesting it exists elsewhere.

## Step 2: Validate Required Components

Read `SKILL.md`, `rubric.md`, `procedure.md`, and `references/evidence-guide.md`.

If the rubric or procedure contains only starter comments, placeholders, or no substantive instructions, refuse to grade.

Do not create missing checks or substitute an improvised evaluation process.

## Step 3: Identify the Package

Record the PR URL in live mode or the bundle identifier in eval mode.

Identify the issue requirements, claimed implementation plan, submitted diff, test evidence, and PR description.

Distinguish directly observed evidence from unsupported claims.

## Step 4: Apply Every Rubric Check

Evaluate all six checks in this exact order:

1. Issue Alignment
2. Plan and Diff Alignment
3. Reproduction and Test Evidence
4. PR Description Accuracy
5. Scope and Repository Standards
6. AI Use Disclosure

For each check:

1. Locate relevant evidence using `references/evidence-guide.md`.
2. Compare that evidence against the check's pass, fail, and unclear conditions.
3. Assign exactly one grade: `pass`, `fail`, or `unclear`.
4. Record one concise evidence line containing the decisive fact, quotation, or missing information.
5. Do not change a grade based on intuition, formatting quality, or the apparent confidence of the PR author.

Complete all six checks even when an earlier check fails.

## Step 5: Review Communication Rules

In live mode, compare the PR title and description against `voice-guide.md`.

Identify any communication-rule violations in the readable summary.

Do not change the verdict solely because of a voice-guide violation unless a rubric check independently establishes a failure.

Skip this step entirely in eval mode.

## Step 6: Determine the Verdict

Apply the verdict rule in `rubric.md`.

- `accept` only if every check is `pass`.
- `reject` if any check is `fail` or `unclear`.

Do not issue conditional acceptance or invent a third verdict.

## Step 7: Produce the Output

Optionally provide a short readable summary of the evidence and any live-mode communication concerns.

Then output one fenced JSON block containing:

- `item`: the PR URL or evaluation bundle ID.
- `checks`: all six checks, with their exact names, grades, and one-line evidence.
- `verdict`: either `accept` or `reject`.

Preserve the field names and order defined in `SKILL.md`.

The fenced JSON block must be the final content. Nothing may follow it.

## Step 8: Final Verification

Before responding, confirm that:

- Exactly one PR package was evaluated.
- Every rubric check was completed.
- Every grade has supporting evidence.
- The verdict follows the rubric without exceptions.
- The JSON is valid and contains no extra fields.
- No text appears after the final fenced JSON block.
