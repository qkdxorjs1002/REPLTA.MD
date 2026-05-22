# Workflow

Write all `__*.md` workflow documents in User language unless the user asks otherwise. Keep them short, practical, and current. Do not add unstated requirements or expand scope without explicit user approval.
Use only the workflow files needed for the task. Workflow files are working notes and may be created or updated before execution approval. Do not change project/source/documentation files until approval when approval is required.
When asking the user any question, use the `request_user_input` tool with concise questions.

## 0. Definition

### Workflow files

- `__SPEEDWAGON.md`: use for recording information found through external searches.
- `__REQ.md`: use to summarize and confirm user requirements when the task requires planning or execution approval.
- `__PLAN.md`: use to describe how the confirmed requirements will be performed. Define implementation specs with stable `SPEC-*` IDs derived from confirmed `REQ-*` IDs.
- `__TASK.md`: use as the active ordered checklist derived from `__PLAN.md` when execution tasks are needed.
- `__TASK.done.md`: use for completed and verified tasks.

### Plan Mode

When operating in Plan Mode, planning comes before implementation. Treat the goal as producing a decision-complete plan, not executing the work.
Plan Mode allows non-mutating exploration and workflow-file updates only.

- Ground the plan in the actual environment before asking questions: inspect relevant files, configs, schemas, docs, and current behavior when they can answer the uncertainty.
- Allowed exploration includes reading files, searching the repository, checking status, reviewing documentation, and running dry-run style commands that do not change tracked work.
- Do not edit project/source/documentation files, generate code into the repository, run formatters that rewrite files, apply migrations, or perform implementation, refactoring, test, or project-documentation changes until the user approves execution.
- If uncertainty still cannot be resolved after investigation, use `request_user_input` to involve the user in the decision-making process, and include 2–3 practical options or recommendations when asking.
- Keep the human in the loop for unresolved decisions: when an open decision affects the plan, ask, incorporate the answer, and repeat until the decision is resolved enough to make the plan executable.
- Keep the implementation plan decision-complete: include the approach, affected interfaces or files when relevant, execution order, edge cases, verification, and explicit assumptions.

## 1. Summarize requirements

Start by summarizing the user's request. When `__REQ.md` is used, record the confirmed requirements there.
Use stable IDs:

- `REQ-001` for confirmed requirements
- `SPEC-001` for implementation specs in `__PLAN.md`
- `TASK-001` for ordered execution tasks in `__TASK.md`
  Requirements must follow these rules:
- Do not add unstated requirements.
- Mark unclear items as questions instead of guessing.
- Do not proceed to planning until the requirements are sufficiently clear.

## 2. Plan the work

When planning is needed, create `__PLAN.md` from `__REQ.md`.
Use Plan Mode for this step. Choose the structure that best fits the task instead of forcing a fixed field template.
The plan must be decision-complete and practical enough to execute, including the implementation approach, affected files or interfaces when relevant, execution order, dependencies, risks or blockers, edge cases, assumptions, and verification approach as needed.
Each implementation spec in `__PLAN.md` must use a stable `SPEC-*` ID and trace back to one or more confirmed `REQ-*` IDs.

## 3. Split the plan into ordered tasks

When execution tasks are needed, create `__TASK.md` as an ordered checklist derived from `__PLAN.md`.
Related tasks may be grouped under ordered Phase headings when that makes execution clearer.
Each task must:

- Reference its source `SPEC-*` ID
- Be actionable
- Be ordered by execution sequence
- Include verification when applicable

```markdown
### Phase 1: Parser
- [ ] TASK-001 Add cursor parser. Source: SPEC-001
- [ ] TASK-002 Add pagination test. Source: SPEC-001

### Phase 2: Integration
- [ ] TASK-003 Wire parser into list endpoint. Source: SPEC-002
```

Treat `__TASK.md` as the active TODO list and update it whenever scope or implementation details change.
When Phase headings are used, keep phases ordered by execution sequence and keep each task under the phase where it will be performed.

## 4. Ask for user approval before execution

Before making implementation, refactoring, test, project-documentation, or multi-file changes, ask the user whether to proceed.

Use the request_user_input tool with a concise approval question.

Do not execute the task list until the user approves.

If the user rejects, revises, or adds requirements:

- Update `__REQ.md` as needed
- Update `__PLAN.md` as needed
- Regenerate or adjust `__TASK.md` as needed
- Ask for approval again before execution

## 5. Execute only after approval

After user approval, work through `__TASK.md` from top to bottom, phase by phase when Phase headings are present.

- Before each task, read the referenced spec and nearby context as needed.
- Check off tasks only after implementation and verification are complete.
- Move completed and verified items to `TASK.done.md`; do not keep duplicate active items in `TASK.md`.
- Keep failed, blocked, or unverified work in `__TASK.md` as actionable follow-up tasks.
- Do not skip tasks unless the reason is recorded.

## 6. Protect the worktree

- Before editing target files, inspect the working tree when possible.
- Do not overwrite user changes.
- Do not commit, push, rebase, reset, or discard changes unless explicitly requested.
- Workflow files are working notes and should not be committed unless explicitly requested.
# Workflow

Write all `__*.md` workflow documents in User language unless the user asks otherwise. Keep them short, practical, and current. Do not add unstated requirements or expand scope without explicit user approval.
Use only the workflow files needed for the task. Workflow files are working notes and may be created or updated before execution approval. Do not change project/source/documentation files until approval when approval is required.
When asking the user any question, use the `request_user_input` tool with concise questions.

## 0. Definition

### Workflow files

- `__SPEEDWAGON.md`: use for recording information found through external searches.
- `__REQ.md`: use to summarize and confirm user requirements when the task requires planning or execution approval.
- `__PLAN.md`: use to describe how the confirmed requirements will be performed. Define implementation specs with stable `SPEC-*` IDs derived from confirmed `REQ-*` IDs.
- `__TASK.md`: use as the active ordered checklist derived from `__PLAN.md` when execution tasks are needed.
- `__TASK.done.md`: use for completed and verified tasks.

### Plan Mode

When operating in Plan Mode, planning comes before implementation. Treat the goal as producing a decision-complete plan, not executing the work.
Plan Mode allows non-mutating exploration and workflow-file updates only.

- Ground the plan in the actual environment before asking questions: inspect relevant files, configs, schemas, docs, and current behavior when they can answer the uncertainty.
- Allowed exploration includes reading files, searching the repository, checking status, reviewing documentation, and running dry-run style commands that do not change tracked work.
- Do not edit project/source/documentation files, generate code into the repository, run formatters that rewrite files, apply migrations, or perform implementation, refactoring, test, or project-documentation changes until the user approves execution.
- If uncertainty still cannot be resolved after investigation, use `request_user_input` to involve the user in the decision-making process, and include 2–3 practical options or recommendations when asking.
- Keep the human in the loop for unresolved decisions: when an open decision affects the plan, ask, incorporate the answer, and repeat until the decision is resolved enough to make the plan executable.
- Keep the implementation plan decision-complete: include the approach, affected interfaces or files when relevant, execution order, edge cases, verification, and explicit assumptions.

## 1. Summarize requirements

Start by summarizing the user's request. When `__REQ.md` is used, record the confirmed requirements there.
Use stable IDs:

- `REQ-001` for confirmed requirements
- `SPEC-001` for implementation specs in `__PLAN.md`
- `TASK-001` for ordered execution tasks in `__TASK.md`
  Requirements must follow these rules:
- Do not add unstated requirements.
- Mark unclear items as questions instead of guessing.
- Do not proceed to planning until the requirements are sufficiently clear.

## 2. Plan the work

When planning is needed, create `__PLAN.md` from `__REQ.md`.
Use Plan Mode for this step. Choose the structure that best fits the task instead of forcing a fixed field template.
The plan must be decision-complete and practical enough to execute, including the implementation approach, affected files or interfaces when relevant, execution order, dependencies, risks or blockers, edge cases, assumptions, and verification approach as needed.
Each implementation spec in `__PLAN.md` must use a stable `SPEC-*` ID and trace back to one or more confirmed `REQ-*` IDs.

## 3. Split the plan into ordered tasks

When execution tasks are needed, create `__TASK.md` as an ordered checklist derived from `__PLAN.md`.
Related tasks may be grouped under ordered Phase headings when that makes execution clearer.
Each task must:

- Reference its source `SPEC-*` ID
- Be actionable
- Be ordered by execution sequence
- Include verification when applicable

```markdown
### Phase 1: Parser
- [ ] TASK-001 Add cursor parser. Source: SPEC-001
- [ ] TASK-002 Add pagination test. Source: SPEC-001

### Phase 2: Integration
- [ ] TASK-003 Wire parser into list endpoint. Source: SPEC-002
```

Treat `__TASK.md` as the active TODO list and update it whenever scope or implementation details change.
When Phase headings are used, keep phases ordered by execution sequence and keep each task under the phase where it will be performed.

## 4. Ask for user approval before execution

Before making implementation, refactoring, test, project-documentation, or multi-file changes, ask the user whether to proceed.

Use the request_user_input tool with a concise approval question.

Do not execute the task list until the user approves.

If the user rejects, revises, or adds requirements:

- Update `__REQ.md` as needed
- Update `__PLAN.md` as needed
- Regenerate or adjust `__TASK.md` as needed
- Ask for approval again before execution

## 5. Execute only after approval

After user approval, work through `__TASK.md` from top to bottom, phase by phase when Phase headings are present.

- Before each task, read the referenced spec and nearby context as needed.
- Check off tasks only after implementation and verification are complete.
- Move completed and verified items to `TASK.done.md`; do not keep duplicate active items in `TASK.md`.
- Keep failed, blocked, or unverified work in `__TASK.md` as actionable follow-up tasks.
- Do not skip tasks unless the reason is recorded.

## 6. Protect the worktree

- Before editing target files, inspect the working tree when possible.
- Do not overwrite user changes.
- Do not commit, push, rebase, reset, or discard changes unless explicitly requested.
- Workflow files are working notes and should not be committed unless explicitly requested.
