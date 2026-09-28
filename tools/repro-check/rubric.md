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
| env-recorded | The repro report's environment record, checked against the issue's stated environment and the Environment section of `references/evidence-guide.md`. | Pass if the report records enough environment information to place the reproduction, including the relevant software/version and OS, plus the tested commit/tag or equivalent version identifier when applicable. If the tested environment differs from the issue's, the difference is stated rather than hidden. | required |
| steps-followable | The repro report's reproduction steps and commands, read with the repo setup instructions described in the Steps section of `references/evidence-guide.md`. | Pass if another person could follow the reported setup and commands in order and reach the tested state without having to guess an important missing action, input, file, option, or configuration. | required |
| behavior-shown | The repro report's expected behavior, observed behavior, and attached or quoted artifact such as terminal output, log, screenshot, or other record, using the Behavior shown section of `references/evidence-guide.md`. | Pass if the package shows what was expected, what actually happened, and provides evidence that directly demonstrates the observed behavior instead of only asserting that the bug occurred. | required |
| behavior-matches-issue | The issue's described failure or behavior compared directly with the repro report's observed behavior and artifacts. | Pass if the behavior demonstrated by the reproduction is the same behavior the issue reports, or the report clearly explains a meaningful tested difference. Fail if the artifact shows an adjacent or unrelated failure and the report claims that the original issue was reproduced. | required |
| outcome-honest | The repro report's stated result, such as reproduced or could not reproduce, read against its steps, environment, and artifacts, using the Honesty section of `references/evidence-guide.md`. | Pass if the stated outcome is supported by the evidence. An evidenced cannot-reproduce passes. A confident reproduction claim fails if the evidence does not actually demonstrate the reported issue. | required |
| claim-specific | The claim comment read against the issue title, issue description, and reported behavior. | Pass if the claim identifies the specific issue or behavior being investigated and states the next artifact or investigation step without promising a guaranteed fix or completion date. It should not be generic enough to fit an unrelated issue. | required |
| repo-conventions | The claim comment and repro report checked against the repo-facts block and the repository communication/contribution rules described in the Comms section of `references/evidence-guide.md`. | Pass if the comments follow applicable repository conventions, including required templates, contribution rules, and any required disclosure of AI assistance. Fail when a relevant repository rule is violated or a required disclosure is omitted. | required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only when every required check passes.

If any required check fails, reject the package.

If a required check is unclear because the available evidence is insufficient to decide whether the condition passes, treat unclear as a failure and reject the package.

A claim-only draft may leave reproduction-only checks not yet applicable; those checks should not be used to reject the claim before reproduction exists. The claim-specific and repo-conventions checks must still pass before the claim is ready to post.