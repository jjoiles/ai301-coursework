# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->
## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | Repro report's environment record, including operating system, relevant runtime/tool versions, and setup details needed to reproduce the issue | Pass if the environment information identifies the relevant system and software context well enough for another person to recreate the reproduction environment. | required |
| Reproduction steps | Repro report's commands and steps, read together with any setup instructions and artifacts | Pass if the stated steps form a complete, executable sequence that another person could follow from the recorded environment to reach the reported outcome without needing unstated essential steps. | required |
| Behavior matches issue | Reproduction artifacts and observed output read against the behavior described in the issue | Pass if the evidence directly tests the specific behavior described in the issue and either demonstrates that behavior or documents a meaningful attempt in which it did not occur. A cannot-reproduce result passes when the attempted trigger is relevant to the issue and the report clearly identifies material conditions or limitations that may explain the different result. Fail if the evidence tests a different or merely adjacent behavior.| required |
| Outcome stated honestly | Pass if the stated outcome accurately reflects the supplied evidence and does not overclaim what was demonstrated. A cannot-reproduce result passes when the report clearly states that result, provides evidence of the attempt, and distinguishes observed facts from possible explanations or untested conditions. Fail when the conclusion contradicts the evidence or claims successful reproduction without supporting evidence.| required |
| Repository conventions | Claim comment and repro comment read against the repository's contribution instructions, templates, AI/disclosure policy, and other applicable repo-facts conventions | Pass if the comments comply with the repository's stated contribution and disclosure requirements, including any required disclosure of AI assistance. If no applicable convention is stated, pass. | required |

## Verdict rule

Accept the package only if every required check passes. Reject the package if any required check fails. Treat unclear evidence for any required check as a failure and reject the package. Preferred checks, if any are added later, do not change the final verdict.
