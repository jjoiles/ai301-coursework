# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I am a student contributor who is still building experience contributing to open-source projects. When I comment on an issue, I want to be clear about what I have actually tested or observed and avoid presenting assumptions as facts. Readers can expect concise updates, specific evidence, and an honest description of what I am investigating.

## Rules I write by

### Rule: Be specific about what I am investigating

I name the issue behavior or scenario I am working on instead of posting a generic claim that I am interested in the issue.

- Wrong: "Hi, I would like to work on this issue."
- Right: "Hi, I'd like to investigate why generated dependency paths under `node_modules/` and `build/` are not being excluded by the technology detector."

### Rule: Do not promise a fix before I understand the problem

I can commit to investigating and reporting what I find, but I do not promise that I will fix the issue or give a completion date before I have reproduced and understood it.

- Wrong: "I'll fix this and have a PR ready tomorrow."
- Right: "I'll reproduce the behavior first and report back with what I find."

### Rule: Separate what I observed from what I think

I state evidence as evidence and clearly label possible explanations instead of presenting guesses as confirmed causes.

- Wrong: "The exclusion logic is definitely broken because it never checks generated directories."
- Right: "I reproduced the reported behavior; next I'll trace the exclusion logic to determine where these generated-directory paths are being allowed through."

### Rule: Report unsuccessful reproduction attempts honestly

If I cannot reproduce an issue, I say so and include the environment, steps, and relevant differences instead of forcing the evidence to support the expected result.

- Wrong: "The bug is confirmed even though I couldn't get the same result."
- Right: "I could not reproduce the reported behavior under this environment; below are the steps I tried and the differences that may be relevant."

### Rule: Keep comments focused on useful evidence

I avoid unnecessary filler and make sure a maintainer can quickly understand what I tried, what happened, and what I plan to investigate next.

- Wrong: "I've been looking at this for a while and tried a bunch of things, but I'm not really sure what is happening."
- Right: "I tested the reported case with the environment and commands below. The behavior reproduced consistently across three runs."

## Things I never post

- A promise that I will fix an issue before I understand its cause.
- A deadline or completion date I cannot guarantee.
- A claim that I reproduced something when my evidence does not show it.
- A guess presented as a confirmed technical cause.
- Generic claim comments that do not mention the specific issue behavior.
- Long filler explanations that make the actual result difficult to find.