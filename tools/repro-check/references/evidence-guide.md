# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives:** In an eval package, look in the repro report's environment record and compare it with the issue context and repo-facts block. In live mode, look at the issue's stated environment or requirements, the repository documentation, and the environment information in the student's draft repro comment.

**What good looks like:** The environment identifies the relevant operating system, runtime or tool versions, dependencies, and setup conditions needed to interpret the reproduction. The versions and conditions should match what the issue targets, or any meaningful differences should be explicitly identified.

## Steps

**Where it lives:** In an eval package, look at the commands and ordered actions in the repro report, together with setup information needed before those actions. In live mode, look at the reproduction steps in the student's draft comment and compare them with any setup or reproduction instructions in the issue.

**What good looks like:** The steps give a stranger a complete path from a stated starting condition to the trigger for the reported behavior. Essential commands, inputs, files, or setup actions are not left unstated.

## Behavior shown

**Where it lives:** In an eval package, look at the repro report's output excerpts, logs, errors, screenshots, test results, or other artifacts and compare them directly with the behavior described in the issue context. In live mode, compare the evidence in the student's draft repro comment with the behavior the GitHub issue says should occur.

**What good looks like:** The evidence demonstrates the same behavior described by the issue rather than a different or merely related failure. For a cannot-reproduce result, the evidence should show that the relevant trigger was attempted under the recorded conditions without producing the reported behavior.

## Honesty

**Where it lives:** In an eval package, compare the repro report's stated outcome with its commands, output, logs, screenshots, errors, and other artifacts. In live mode, compare the conclusion in the student's draft comment with the evidence the student plans to post.

**What good looks like:** The conclusion says only what the evidence supports. A successful reproduction is backed by evidence of the issue's behavior, while an honest cannot-reproduce accurately reports that the attempted steps did not produce it and does not claim more than was observed.

## Comms

**Where it lives:** In an eval package, compare the claim comment and repro report with the issue context, repo-facts block, contribution instructions, comment or PR templates, and any AI-use or disclosure policy. In live mode, check the GitHub issue thread and repository documentation against the student's draft claim and repro comments.

**What good looks like:** The claim identifies the specific issue and promises investigation rather than guaranteeing a fix or deadline. The repro comment is specific to the observed work, follows applicable repository conventions, and satisfies any required AI-assistance disclosure. Boilerplate that ignores issue-specific facts or required disclosure does not pass.