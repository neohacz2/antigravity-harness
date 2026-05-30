# Superpowers for Antigravity

This profile adapts Superpowers workflows for Antigravity with strict single-flow execution for the Harness Engineering Template project.

## Core Rules

1. Prefer local skills in `.agent/skills/<skill-name>/SKILL.md`.
2. Execute one core task at a time with `task_boundary`.
3. Track checklist progress in `<project-root>/docs/plans/task.md` (table-only live tracker).
4. Follow strict single-flow execution and verify all changes before completion.

## Spec-Driven Development (SDD) Workflow

### Workflow Phases
Ideate → Define → Sketch → Plan → Build → Compound

| Phase | Skill | 산출물 |
|---|---|---|
| Ideate | `idea-refine` | `artifacts/<feature>/idea.md` (선택) |
| Specify | `write-spec` | `artifacts/<feature>/spec.md` |
| Sketch | `sketch-wireframe` | `artifacts/<feature>/wireframe.html` |
| Plan | `draft-plan` | `artifacts/<feature>/plan.md` |
| Build | `execute-plan` | `artifacts/<feature>/learnings.md` |
| Compound | `compound` | — |

## Development Workflow

- Package Manager: `bun`
- Commit Rules: Follow Conventional commits, commit by feature units.

## Testing & Verification

Acceptance criteria must be defined and proven before claiming completion.

| Command | Scope |
| :--- | :--- |
| `bun run test` | Vitest Unit/Integration Tests |
| `bun run test:watch` | Vitest Watch Mode |
| `bun run test:e2e` | Playwright E2E Tests |

## Architecture & Dependency Rules

To prevent circular dependencies, reverse dependencies are strictly forbidden. Always implement from the lowest layer upwards.

| Layer | Directory | Allowed Dependencies |
| :---: | :--- | :--- |
| 1 | `types/` | None |
| 2 | `config/` | types |
| 3 | `lib/` | types, config |
| 4 | `services/` | types, config, lib |
| 5 | `hooks/` | types, config, lib, services |
| 6 | `components/` | types, config, lib, hooks |
| 7 | `app/` | All layers allowed |
