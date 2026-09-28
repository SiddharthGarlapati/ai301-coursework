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

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

### Where it lives

In an eval package, look at the repro report's environment information and compare it with the issue context and the repo-facts block.

In live mode, look at the issue's stated environment or affected version, the repository's README or setup documentation, release/version information when relevant, and the environment recorded in the draft repro comment.

### What good looks like

The environment identifies the relevant software or application version and operating environment needed to place the reproduction. When applicable, it also identifies the tested commit, tag, runtime, or toolchain.

The tested version should match the issue's target version, or the report should clearly state and explain the difference.


## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

### Where it lives

In an eval package, look at the reproduction steps and commands in the repro report, together with setup information in the repo-facts block.

In live mode, compare the draft reproduction steps with the repository's README, CONTRIBUTING documentation, or other documented setup instructions.

### What good looks like

Another person should be able to start from the stated environment, follow the commands and actions in order, and reach the condition being tested without guessing an important missing input, file, option, configuration, or setup action.

The steps should test the behavior described by the issue rather than a different path that happens to fail.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

### Where it lives

In an eval package, compare the issue's description of the expected failure with the repro report's expected behavior, observed behavior, and artifacts such as terminal output, logs, screenshots, or other recorded results.

In live mode, read the issue description and compare it directly with the evidence included or linked in the draft repro comment.

### What good looks like

The report makes the difference between expected and observed behavior clear, and the artifact directly supports what the report says happened.

The behavior demonstrated by the artifact should match the behavior described by the issue. A different error, exit code, exception, or failure path does not prove the reported issue unless the difference is explicitly explained and relevant.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

### Where it lives

In an eval package, compare the repro report's final claim or result with its environment, steps, observed behavior, and artifacts.

In live mode, compare statements such as "reproduced," "could not reproduce," or similar conclusions with the actual evidence included in the draft.

### What good looks like

The conclusion says exactly what the evidence supports.

A report that says "could not reproduce" is valid when it records what was tested and shows the observed result. A report should not claim successful reproduction when its evidence shows a different failure or does not demonstrate the issue's behavior.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->
### Where it lives

In an eval package, look at the claim comment and repro comment together with the issue context and repo-facts block, especially repository contribution rules, templates, and disclosure requirements.

In live mode, check the issue thread and the repository's README, CONTRIBUTING file, issue templates, AGENTS.md or similar contributor instructions, and any stated AI-assistance policy before evaluating the draft comment.

### What good looks like

The claim identifies the specific behavior being investigated and states the next investigation or evidence step instead of making a generic request to be assigned.

The comments follow repository-specific contribution requirements, including required templates or AI-use disclosures when present. They do not promise an unverified fix, claim results beyond the evidence, or ignore a relevant repository rule.
