# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

### Where it lives

In an eval package, look at:

- the issue context for the reported behavior and requested outcome;
- the repro-evidence block for the commands, inputs, observations, logs, and outputs that demonstrate the failure;
- the candidate plan's stated diagnosis or cause;
- the candidate plan's proposed approach when it makes claims about where the defect lives.

In live mode, look at:

- the repro evidence quoted or summarized in the draft `plan.md`;
- the diagnosis stated in `plan.md`;
- the proposed approach in `plan.md`;
- the issue thread only when it is provided or available as part of the grading request.

### What good looks like

The stated diagnosis explains behavior that the repro evidence actually shows.

The diagnosis must not contradict the reproduced behavior, ignore evidence that points elsewhere, or introduce a cause that is unsupported by the evidence included in the package or draft.

If the evidence points to a cause upstream from the visible failure, the proposed fix should address that supported cause rather than only hiding the final symptom.

## Scope

### Where it lives

In an eval package, look at:

- the issue context for what change is being requested;
- the candidate plan's in-scope statement;
- the candidate plan's out-of-scope or not-in-scope statement;
- the files, components, or areas the plan says will change;
- the proposed approach for any additional work that may not appear directly in the scope statement;
- the repo-facts block when repository boundaries or conventions affect the allowed scope.

In live mode, look at:

- the scope described in `plan.md`;
- what `plan.md` explicitly says will not be changed;
- the files or areas named in `plan.md`;
- the proposed approach in `plan.md`;
- the issue thread when it contains explicit maintainer limits on scope.

### What good looks like

The plan describes one bounded and reviewable change.

Every proposed file, component, or behavior change should directly support the issue being addressed.

The plan should clearly state what is outside the change so that unrelated refactors, renaming, migrations, cleanup, redesigns, or feature expansion do not silently enter the work.

A plan may intentionally solve only part of a larger issue if that boundary is stated clearly and does not conflict with maintainer direction.

## Executability

### Where it lives

In an eval package, look at:

- the candidate plan's named files or areas;
- the proposed implementation approach;
- any stated order of work;
- the repo-facts block when it identifies relevant repository structure, components, commands, or conventions.

In live mode, look at:

- the files or areas named in `plan.md`;
- the part of `plan.md` that explains how the change will be implemented;
- the order or sequence of work described in `plan.md`, if one is needed;
- relevant repository facts only when they are explicitly provided or referenced by the plan.

### What good looks like

Another contributor should be able to begin the implementation without asking the author where to start or what behavior is supposed to change.

The plan should identify enough of the implementation path that a stranger can determine:

- what file or component to inspect;
- what behavior needs to change;
- what implementation direction to follow.

The plan does not need to specify every line of code, but it must provide a concrete implementation direction rather than a vague intention.

## Test plan

### Where it lives

In an eval package, look at:

- the repro-evidence block's commands, inputs, steps, observed failure, and outputs;
- the part of the candidate plan that describes how the reproduced behavior will be tested again;
- the candidate plan's stated expected result after the fix;
- any additional regression tests or repository test commands named in the package.

In live mode, look at:

- the repro evidence quoted or summarized in `plan.md`;
- the part of `plan.md` that describes how the reproduced behavior will be re-run after the change;
- the expected after-fix behavior stated in `plan.md`;
- any relevant repository test command or test file explicitly named in the plan.

### What good looks like

The test plan must connect directly to the reproduced behavior.

It should identify the same repro input or an equivalent real-code check and state an observable result that should be different after the fix.

A decisive test plan lets another person compare:

- what happened before;
- what they should run after the change;
- what result they should expect to observe.

Statements such as "run the tests," "test manually," or "verify that it works" are not sufficient by themselves unless they also identify the specific behavior and expected outcome that proves the issue is fixed.

Additional regression tests are useful, but they do not replace showing that the originally reproduced behavior changed as intended.

## Honesty

### Where it lives

In an eval package, look at:

- the candidate plan's stated risks;
- the candidate plan's unknowns and assumptions;
- claims in the diagnosis or approach that are not fully established by the repro evidence;
- the `## Deviations` section when the package represents a plan after implementation;
- the issue context or repo-facts block when they reveal unresolved constraints.

In live mode, look at:

- the risks and unknowns stated in `plan.md`;
- assumptions made in the diagnosis or approach;
- unresolved information visible in the issue context when it is provided;
- the completed `## Deviations` section after the implementation is finished.

### What good looks like

Claims supported by evidence should be stated as established facts.

Questions that are not yet resolved should be identified as unknowns, assumptions, or risks rather than presented with false certainty.

If implementation later differs from the original plan, the meaningful difference and the reason for it should be recorded under `## Deviations`.

If the implementation follows the plan without meaningful changes, that should also be stated explicitly rather than leaving `## Deviations` blank.

## Comms

### Where it lives

In an eval package, look at:

- the candidate plan comment;
- the issue context and thread highlights;
- the candidate plan;
- the repo-facts block, including contribution instructions, templates, conventions, workflow requirements, and AI-use disclosure requirements when present.

In live mode, look at:

- the draft `comment.md`;
- the corresponding `plan.md`;
- the issue thread when it is provided or accessible as part of the grading request;
- repository contribution rules when they are explicitly available to the skill or included in the grading context.

### What good looks like

The plan comment should accurately represent the work described in the plan.

It should acknowledge relevant maintainer instructions and should not promise changes, files, features, or tests that are absent from `plan.md`.

If the issue thread or repository states an explicit constraint, such as:

- keeping an API unchanged;
- using a particular testing approach;
- following a contribution template;
- following a repository workflow;
- disclosing AI assistance;

the plan comment and plan should respect that constraint.

A generic comment such as "I can fix this, please assign me" is not enough when the issue thread contains specific direction the contributor is expected to address.