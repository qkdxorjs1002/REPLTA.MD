# REPLTA.MD

[한국어](README.ko.md)

This repository contains working rules for how an agent should operate inside a project. The central document is `AGENTS.md`, and `config.toml` supports the default agent runtime configuration.

## Core Philosophy

The philosophy in `AGENTS.md` favors controlled execution over rushing into changes. Requirements are clarified first, then a plan is written, and only after user approval are actual changes made. This flow is not ceremony for its own sake; it is a safeguard against guessed scope, accidental expansion, and damage to user-owned changes.

The document emphasizes these principles:

- Requirements are recorded with `REQ-*` IDs so the agreed scope stays explicit.
- Implementation direction is described with `SPEC-*` IDs, connecting requirements to execution.
- Execution work is split into `TASK-*` IDs so ordering and verification are visible.
- Planning and execution are separated, and project file changes require user approval first.
- The repository's actual state is inspected before acting to reduce unnecessary assumptions.
- Completed work and remaining work are separated so current progress stays traceable.
- Changes made by the user or other tools must not be reverted or overwritten.

## Workflow Documents

`AGENTS.md` defines these workflow documents for use when needed:

- `__REQ.md`: requirement summary and confirmation
- `__PLAN.md`: execution plan connected to requirements
- `__TASK.md`: active work list
- `__TASK.done.md`: completed and verified work list
- `__SPEEDWAGON.md`: notes from external searches

These files are treated as working notes. The principle is to create only what is needed and keep it short, practical, and current.

## Repository Layout

- `AGENTS.md`: agent work rules and approval-based workflow
- `config.toml`: model, reasoning effort, personality, and feature flag settings

## Application Guide

### Global

- Apply `AGENTS.md` to `~/.codex/AGENTS.md`.
- Merge `config.toml` into `~/.codex/config.toml`.

### Project

- Apply `AGENTS.md` to the workspace `./AGENTS.md`.
- Merge `config.toml` into `./.codex/config.toml`.

For `config.toml`, merge the relevant settings into the existing file instead of replacing unrelated local configuration.

## Operating View

The rules in this repository treat the agent as a collaborator, not an independent executor. The agent should read context first, turn uncertainty into questions, get approval before making changes, and report verification results after execution. Good work is therefore not just a changed file; it is a traceable state that shows why the change was made and which requirements it satisfied.
