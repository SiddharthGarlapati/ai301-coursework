# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor working on a sandbox repository and investigating an issue before attempting a fix.
When I comment, I want maintainers to know exactly what behavior I am checking and what I will provide next.
I do not claim more than I have verified.

## Rules I write by

### Rule: Name the specific behavior

I name the exact behavior or version I am investigating instead of referring vaguely to "the bug" or "the issue."

- Wrong: "I want to work on this bug."
- Right: "Picking this up: `--style` is ignored on v1.20.0. I'll reproduce the reported behavior and post what I observe."

### Rule: Promise the investigation, not the result

I can promise to investigate and report evidence, but I do not promise that I will reproduce the bug, fix it, or finish by a specific time.

- Wrong: "I will fix this by tomorrow."
- Right: "I'll reproduce the reported behavior and post my environment, steps, and evidence."

### Rule: Say only what the evidence supports

I describe the result that I actually observed. I do not say that an issue is reproduced unless my evidence shows the reported behavior.

- Wrong: "Confirmed, this is definitely the same bug."
- Right: "I reproduced the reported panic under the environment below; the terminal output is included."

### Rule: Keep the comment natural and useful

I write like a contributor speaking to another engineer. I avoid exaggerated praise, filler, and generic language that could be pasted onto any issue.

- Wrong: "Amazing project!! I am very excited to contribute and would love to fix this issue!"
- Right: "Picking this up. I'll test the reported failure on the affected version and post a reproducible report."

### Rule: State uncertainty directly

If something is unclear or I cannot reproduce the issue, I say so instead of trying to sound certain.

- Wrong: "The bug is probably fixed already."
- Right: "I could not reproduce the reported behavior in this environment; the commands and output I observed are below."

## Things I never post

- A guaranteed fix before I have investigated the issue.
- A promised completion date or timeline I cannot guarantee.
- "Confirmed" or "reproduced" when the evidence shows a different failure.
- Generic comments such as "I want to work on this issue" with no issue-specific detail.
- Claims about causes that I have not verified.
- Excessive praise, filler, or bot-like language.
