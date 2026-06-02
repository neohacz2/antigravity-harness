# Superpowers for Antigravity

This profile adapts Superpowers workflows for Antigravity with strict single-flow execution for the Harness Engineering Template project.

## Core Rules

1. **How to Find & Use Skills**:
   - 로컬에 존재하는 11개의 스킬(`.agent/skills/<skill-name>/SKILL.md`)을 활용합니다.
   - **스킬 로딩 원칙**: 유저의 요청이나 해결하려는 문제에 특정 스킬이 적용될 가능성이 **1%라도 있다면, 어떠한 작업이나 답변(질문 포함)을 하기 전에 반드시 해당 `SKILL.md`를 `view_file`로 먼저 호출**하여 지침을 엄격히 준수해야 합니다.
2. Execute one core task at a time with `task_boundary`.
3. Track checklist progress in `<project-root>/docs/plans/task.md` (table-only live tracker).
4. Follow strict single-flow execution and verify all changes before completion.

## Available Skills (11 Local Skills)

현재 프로젝트에는 아래 11개의 스킬만 존재하며, 각 스킬은 상황에 맞게 우선적으로 로드되어 작동 가이드 역할을 수행합니다.

### 1. Spec-Driven Development (SDD) Workflow Skills
| Phase | Skill | 산출물 | 설명 |
|---|---|---|---|
| Ideate | `idea-refine` | `artifacts/<feature>/idea.md` (선택) | 날것의 아이디어를 실행 가능한 MVP 범위의 기획으로 다듬습니다. |
| Specify | `write-spec` | `artifacts/<feature>/spec.md` | 기능의 불변 조건(Invariants)과 사용자 시나리오(WHAT)를 정의합니다. |
| Sketch | `sketch-wireframe` | `artifacts/<feature>/wireframe.html` | 스펙 검증을 위한 HTML 레이아웃 와이어프레임을 스케치합니다. |
| Plan | `draft-plan` | `artifacts/<feature>/plan.md` | spec.md 기반의 TDD 태스크 리스트와 구현 계획을 생성합니다. |
| Build | `execute-plan` | `artifacts/<feature>/learnings.md` | TDD 규율에 따라 계획을 단일 태스크 단위로 구현 및 검증합니다. |
| Compound | `compound` | — | 완료된 피처들에서 누적된 학습(learnings)을 통해 규칙/원칙을 갱신합니다. |

### 2. Engineering & Best Practice Skills
| Skill | 설명 | 언제 사용하는가 |
|---|---|---|
| `next-best-practices` | Next.js 15/16 및 RSC(서버 컴포넌트) 모범 사례 | Next.js 서버/클라이언트 아키텍처, 데이터 페칭, 파일 컨벤션 작업 시 |
| `shadcn` | shadcn/ui 컴포넌트 관리 및 구성 | 컴포넌트 초기화, 추가, 스타일 및 구성 요소의 조합 변경 시 |
| `vercel-composition-patterns` | React 컴포넌트 합성(Composition) 패턴 | 컴포넌트의 유연성 확보 및 아키텍처 설계 시 |
| `vercel-react-best-practices` | Vercel의 성능 최적화 및 렌더링 최적화 지침 | 성능 병목 해결, 렌더링 최적화, 번들 최소화 작업 시 |
| `web-design-guidelines` | 웹 인터페이스 및 UX 가이드라인 준수 감사 | 완성된 UI/UX 검토, 접근성(a11y) 감사 및 시각 디자인 개선 시 |

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
