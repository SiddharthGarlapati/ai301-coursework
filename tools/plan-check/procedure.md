# Procedure: how this skill grades a plan package

## Read order

1. Read the issue context first.
   - Record the reported problem.
   - Record the requested outcome.
   - Record any explicit maintainer instructions or constraints.
   - Do not grade any checks yet.

2. Read the repo-facts block next, if one is provided.
   - Record any repository rules that affect scope, implementation, testing, contribution workflow, templates, or AI-use disclosure.
   - In live mode, use repository guidance only when it is available as part of the grading context.

3. Read the repro-evidence block before reading the candidate plan's diagnosis.
   - Record the exact behavior that was reproduced.
   - Record the commands, inputs, or steps used.
   - Record the relevant observed output.
   - Record what the reproduction proves.
   - Record anything the reproduction does not prove.

4. Read the candidate plan completely.
   - Record the stated diagnosis or cause.
   - Record what is in scope.
   - Record what is explicitly out of scope.
   - Record the files, components, or areas the plan proposes changing.
   - Record the implementation approach.
   - Record how the reproduced behavior will be tested again.
   - Record the expected after-fix result.
   - Record risks, assumptions, and unknowns.
   - Record the `## Deviations` entry when the plan is being checked after implementation.

5. Read the candidate plan comment after reading the full plan.
   - Record what the comment promises to change.
   - Record what it says about the cause.
   - Record what it says about testing.
   - Record whether it responds to maintainer instructions.

6. Compare the notes from the issue, repro evidence, repo facts, plan, and comment before grading.
   - When two sources disagree, use the actual supplied evidence rather than assuming which one is correct.
   - Do not add facts that are not present in the package.

## Evidence gathering

1. For diagnosis and grounding:
   - Find the diagnosis stated in the candidate plan.
   - Find the specific observations in the repro-evidence block that support or contradict that diagnosis.
   - Record whether the reproduced behavior actually points to the stated cause.
   - Record any important repro evidence that the diagnosis ignores.

2. For root-cause targeting:
   - Identify where the failure becomes visible.
   - Identify where the plan says the cause lives.
   - Identify where the proposed fix will be made.
   - Record whether the proposed change addresses the evidence-supported cause or only hides the visible symptom.

3. For scope:
   - Record the plan's in-scope statement.
   - Record the plan's out-of-scope or not-in-scope statement.
   - List every file, component, API, behavior, refactor, cleanup, migration, documentation change, or other area the plan proposes touching.
   - Compare those changes with the issue request.
   - Mark any proposed work that is unrelated to the issue or outside the stated boundary.

4. For executability:
   - Record the file or component where the implementation should begin.
   - Record the behavior that will change.
   - Record the implementation direction.
   - Record any required order of work.
   - If a contributor would still need to ask where to start or what to change, record what information is missing.

5. For the test plan:
   - Record the original repro command, input, step, or observable behavior.
   - Record the before-fix result from the repro evidence.
   - Record how the candidate plan says the behavior will be tested again.
   - Record the expected after-fix result.
   - Record any additional regression test or repository test command the plan names.

6. For honesty:
   - Identify claims in the diagnosis or approach that are not fully established by the repro evidence.
   - Check whether those claims are presented as facts, assumptions, risks, or unknowns.
   - Record any unresolved issue or repository constraint.
   - If grading after implementation, check whether meaningful changes from the original plan are recorded under `## Deviations`.

7. For communication:
   - Compare the candidate plan comment with the candidate plan.
   - Compare both with explicit maintainer directions in the issue context or thread highlights.
   - Compare both with applicable repo-facts.
   - Record any promise in the comment that is not supported by the plan.
   - Record any maintainer instruction or repository rule that the comment or plan ignores.

8. Use `references/evidence-guide.md` whenever the correct evidence location is uncertain.
   - Do not invent missing evidence.
   - Do not use outside knowledge to fill a gap in the package.

## Check execution

1. Grade the checks in this order:
   1. `diagnosis-grounded`
   2. `root-cause-targeted`
   3. `bounded-scope`
   4. `executable-by-a-stranger`
   5. `test-decisive`
   6. `uncertainty-honest`
   7. `thread-and-repo-aligned`

2. For each check, use only:
   - the evidence named in that rubric row;
   - the evidence gathered using `references/evidence-guide.md`.

3. Grade a check `pass` when the available evidence satisfies the complete pass condition.

4. Grade a check `fail` when the available evidence clearly violates the pass condition.
   - A direct contradiction between the candidate plan and the repro evidence counts as a fail.
   - Work clearly outside the stated scope counts as a fail.
   - A test that cannot show an observable before-and-after difference counts as a fail.

5. Grade a check `unclear` when the evidence needed to decide is genuinely missing or ambiguous.
   - Do not guess.
   - Do not assume missing facts are true.
   - Do not automatically call missing evidence a fail unless the available evidence clearly proves the pass condition is violated.

6. Record a short reason for every grade.
   - Use concrete evidence from the package.
   - Quote or identify the smallest useful part of the candidate plan, repro evidence, thread, or repo facts that supports the grade.

7. Do not let one strong check compensate for another failed required check.
   - Grade every required check independently.

8. Once the needed evidence for a check has been gathered, use those recorded facts to grade it.
   - Re-read the source only when two pieces of gathered evidence conflict or when a quote needs verification.

## Verdict assembly

1. Collect the final grade for every rubric check.

2. Apply the verdict rule from `rubric.md` exactly.

3. Return `accept` only when every required check is `pass`.

4. Return `reject` when any required check is:
   - `fail`; or
   - `unclear`.

5. Preferred checks, if any are added later, may produce feedback but must not change the final verdict.

6. When the verdict is `reject`, identify the required failed or unclear check or checks that caused the rejection.

7. For each deciding check, quote or clearly identify the package evidence that caused the grade.
   - Prefer the candidate plan's own wording and the repro, thread, or repo evidence it conflicts with or fails to satisfy.

8. Make sure the check names in the output exactly match the check names in `rubric.md`.

9. End with the required binary verdict:
   - `accept` if the plan is ready to post and build from;
   - `reject` if it is not.

10. Before returning the result, verify that the final verdict matches the per-check grades and the verdict rule.
    - Never return `accept` when a required check is `fail` or `unclear`.