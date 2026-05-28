# Workflow

Write workflow documents in the user's language unless asked otherwise. Keep them short, practical, and current. Do not add unstated requirements or expand scope without explicit user approval.

## 0. Core Rules

- Active workflow files live under `.agent-workflow/`.
- Do not modify source, tests, docs, configs, migrations, generated files, or other durable project artifacts before execution approval.
- Workflow files may be created or updated before execution approval.
- Do not commit, push, rebase, reset, discard changes, or include workflow files in commits unless explicitly requested.
- Check the worktree before and after work when practical. Never overwrite user changes.
- Keep active workflow files as current-state snapshots, not logs.

## 1. Request Startup

At the start of every non-trivial user request, inspect `.agent-workflow/` if it exists.

- If active workflow files contain remaining actionable work, use `request_user_input` before starting the new request.
- Ask whether to:
  1. do the remaining work first,
  2. combine it with the new request,
  3. defer or archive it,
  4. discard the active workflow and start fresh.
- If no actionable work remains but active workflow files are still present, archive them before continuing.

## 2. Workflow Files

Use only the files needed for the current task.

- `.agent-workflow/request.md`: confirmed requirements, assumptions, open questions, out-of-scope items, and relevant references.
- `.agent-workflow/plan.md`: approved or proposed execution plan.
- `.agent-workflow/task.md`: current executable tasks.
- `.agent-workflow/task.recent.md`: recently completed tasks and verification summary.
- `.agent-workflow/speedwagon.md`: external findings that affect requirements, specs, tasks, or verification.
- `.agent-workflow/archive/<timestamp>-<task-slug>/`: archived workflow history.

## 3. Requirements

For complex or approval-requiring work, create or update `.agent-workflow/request.md`.

Before finalizing requirements:

- Search relevant workflow archives when they may contain useful prior context.
- Inspect repository files, documentation, or tools instead of guessing.
- Record concise references and confirmed facts only.
- Assign stable requirement IDs: `REQ-001`, `REQ-002`, etc.
- Keep assumptions and open questions separate.
- Do not finalize planning until requirements are clear enough to execute safely.

## 4. Plan Mode

Planning comes before implementation.

Use Plan Mode to create or update `.agent-workflow/plan.md`.

The plan must include only what is needed:

- objective,
- constraints and assumptions,
- selected approach,
- affected files or interfaces,
- execution order,
- risks and edge cases,
- validation strategy,
- items requiring approval.

Assign stable spec IDs: `SPEC-001`, `SPEC-002`, etc.
Each `SPEC-*` must trace to one or more `REQ-*`.

Use `request_user_input` when plan choices materially affect scope, risk, compatibility, cost, or implementation direction. Revise `plan.md` after user feedback.

## 5. Tasks

After the plan is clear, create or update `.agent-workflow/task.md`.

- Split work into phases and tasks.
- Assign stable task IDs: `TASK-001`, `TASK-002`, etc.
- Each task must reference its source `SPEC-*`.
- Each task should include verification when applicable.
- Use explicit states: `Pending`, `In Progress`, `Completed`, `Blocked`, or `Skipped`.
- Keep `task.md` focused on the current execution window and next useful step.

Before implementation starts, use `request_user_input` to ask whether to execute the prepared `task.md`.

## 6. Execution

After approval, execute tasks phase by phase.

- Execute approved tasks from top to bottom.
- Mark a task `Completed` only after implementation and verification are done.
- Mark blocked work as `Blocked` with the next required action.
- Keep blocked, skipped, pending, or unverified work in `task.md`.
- Move completed and verified work to `task.recent.md`, then remove it from `task.md`.
- If scope or implementation changes materially, update workflow files and ask the user before continuing.

## 7. External Findings

When external search or documentation review affects the task, record only decision-relevant findings in `.agent-workflow/speedwagon.md`.

Each entry should be concise:

- source or link,
- key finding,
- related `REQ-*` or `SPEC-*`,
- impact on the current decision.

Do not store raw search dumps, long candidate lists, or stale findings.

## 8. Archiving

Archive workflow files when:

- no actionable tasks remain,
- a workflow is superseded,
- the user chooses to archive or discard remaining work,
- active files are stale but no longer needed.

Archive to:

`.agent-workflow/archive/<timestamp>-<task-slug>/`

Include existing workflow files and a concise `summary.md` with:

- original request,
- final requirements summary,
- selected plan,
- completed tasks,
- verification results,
- blocked, skipped, or remaining work.

After successful archiving, active workflow files should be removed or cleared unless the user explicitly asks to keep them.

## 9. Completion Report

When work finishes, report briefly:

- changed files and behavior,
- verification commands and results,
- remaining risks or blocked work,
- whether workflow files were archived.
