# Harness Learning Log Workflow

Date: 2026-05-29

## Task Summary

Added a project-wide Harness rule requiring every completed PocketNode task to
record the concrete skills learned during the task.

## Skills Practiced

- Harness workflow design.
- Academic learning-log design.
- Documentation-driven done definitions.
- Trace and validation template design.

## What Was Learned

A learning requirement should live in the same operational surfaces agents
already use to finish work. Putting it only in a product spec is too weak
because future agents may work from story packets, validation reports, traces,
or Harness docs instead.

## Implementation Details

The workflow was added to the Harness done definition, task loop, trace
guidance, story template, validation report template, and a new `docs/learning/`
area. This makes learning evidence part of the normal completion path.

## Tradeoffs And Limits

The current Harness CLI trace schema does not have a dedicated `learning_note`
field. Until that exists, traces should include the learning note path in
`notes` or `files_changed`.

## Validation Evidence

- Reviewed affected Harness docs and templates.
- Ran placeholder scan against the updated files.
- Ran `git diff --check`.

## Reusable Guidance

When future tasks complete, write the learning note after validation, when the
real lesson is known. Keep the note concrete: name the skill, the project files
that made the skill real, the proof command, and what the next task should reuse.
