# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The candidate plan's stated diagnosis read against the issue context and the repro-evidence block, especially the observed behavior, commands, and outputs. | Pass when the stated cause explains the reproduced behavior and does not contradict or ignore evidence in the repro. The diagnosis must be supported by what was actually observed rather than by an unsupported guess. | required |
| root-cause-targeted | The plan's diagnosis and proposed approach read against the repro evidence and the point where the failure is observed. | Pass when the proposed change addresses the cause supported by the evidence rather than only hiding, catching, or repainting the visible symptom. A smaller fix is acceptable when it intentionally addresses the supported cause and clearly states its boundary. | required |
| bounded-scope | The plan's in-scope and out-of-scope statements, named files or areas, proposed approach, and the issue's requested change. | Pass when the work is one reviewable change with a clear boundary. Every proposed file or area must contribute directly to that change, and unrelated cleanup, redesign, migration, renaming, or "while I'm here" work must be excluded. | required |
| executable-by-a-stranger | The plan's files or areas, implementation approach, and order or description of the work, read with any relevant repo-facts. | Pass when another contributor could begin the implementation from the plan without needing the author to explain what file or component to inspect, what behavior to change, or what implementation direction to follow. | required |
| test-decisive | The candidate plan's test plan read against the repro-evidence block's commands, inputs, observed failure, and artifacts. | Pass when the test plan exercises the behavior demonstrated by the repro and states an observable expected result after the fix. A generic instruction such as "run the tests" or "verify it works" is not sufficient by itself. | required |
| uncertainty-honest | The plan's risks, unknowns, assumptions, and Deviations section, read against unresolved facts visible in the issue, repro evidence, and repo-facts. | Pass when material unknowns or assumptions are stated as unknowns instead of facts, risks that could affect implementation are acknowledged, and any known difference between the plan and the work performed is recorded honestly. If no material uncertainty is visible, the plan must still avoid unsupported certainty. | required |
| thread-and-repo-aligned | The draft plan comment read against the issue thread or thread highlights, the candidate plan, and the repo-facts block including contributing instructions, templates, conventions, and AI-use disclosure requirements when present. | Pass when the comment accurately represents the plan, responds to explicit maintainer direction, follows applicable repository contribution rules, and does not promise work outside the plan. Boilerplate that ignores relevant thread or repo instructions fails. | required |

## Verdict rule

Accept only when every required check passes.
A grade of `unclear` on any required check counts as a failure because the package does not provide enough evidence to safely post and build from the plan.
Any failed or unclear required check produces `reject`.
Preferred checks, if any are added later, may provide feedback but never change the final verdict.
