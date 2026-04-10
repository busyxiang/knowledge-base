## Global Config (CLAUDE.md)

### Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it via subagents
- One task per subagent for focused execution

## Agent Team Template

A prompt template for spawning a coordinated multi-agent team to implement a feature end-to-end. Fill in `{{placeholders}}` before use.

### Placeholders

| Placeholder | Example |
|---|---|
| `{{feature-name}}` | Cart discount apply flow |
| `{{ticket}}` | JIRA-1234 |
| `{{fe-repo-path}}` | /Users/me/repos/frontend |
| `{{fe-worktree}}` | feat/cart-discount |
| `{{be-repo-path}}` | /Users/me/repos/backend |
| `{{be-worktree}}` | feat/cart-discount |
| `{{base-branch}}` | staging |
| `{{submodule-base}}` | master (if submodule changes needed) |

### Template

```
I need to work on {{feature-name}}. Create an agent team to implement the required changes. Spawn the following members:

---

### Phase 1 — Planning & Design

**Planner**
- Gather and compile requirements from {{ticket}} and all its subtasks/child issues
- Run /jira to pull ticket details and acceptance criteria
- Draft the implementation plan, then discuss with Architect and Security
- Finalize the plan → share with all agents → get sign-off → present to user for approval before Phase 2 begins

**Architect** (use senior-architect skill)
- Review Planner's draft for feasibility, scalability, and separation of concerns
- Define API contracts (endpoints, request/response shapes, error codes)
- Identify database schema changes if any
- Publish contracts for Frontend and Backend to consume
- During Phase 2, remain available to clarify contracts and review architectural decisions
- During Phase 3, review Backend's architecture choices and Frontend's integration patterns

**Security** (use senior-security skill)
- Review Architect's design for auth, input validation, injection, and data exposure risks
- Flag issues as blocking or advisory — blocking issues must be resolved before Phase 2
- During Phase 2, remain available to review sensitive implementation paths flagged by Backend
- During Phase 3, review auth and data-handling code in both PRs before they are finalized

> **Phase 1 exit criteria:**
> - Plan signed off by Planner + Architect + Security
> - API contracts documented
> - No blocking security issues open
> - **User must approve the plan before proceeding to Phase 2** — do not start implementation until user gives explicit go-ahead
> - If the user requests changes or provides feedback, the relevant agents (Planner, Architect, Security) must revise → re-discuss → re-present. Repeat until the user approves
> - If the user rejects the plan entirely, all agents discard current work and restart planning from scratch based on user's new direction

---

### Phase 2 — Implementation

**Frontend** (use senior-frontend skill)
- Work in {{fe-repo-path}} using worktree {{fe-worktree}}, branch off from {{base-branch}}
- Implement against API contracts from Phase 1
- During Phase 1, may start non-functional scaffolding only (layout, component stubs, type definitions) — no business logic until user approves the plan
- When Backend signals readiness, switch to real integration and report any contract mismatches

**Backend** (use senior-backend skill)
- Work in {{be-repo-path}} using worktree {{be-worktree}}, branch off from {{base-branch}}
- If submodule changes needed, branch submodule off from {{submodule-base}}
- Implement API endpoints per Architect's contracts, coordinating with Security on sensitive paths
- When endpoints are ready, notify Frontend and address any integration issues they raise
- Use /sonar-verify-branch to check code quality during development
- Generate and update tests for new changes

> **Phase 2 exit criteria:**
> - Frontend successfully calls Backend endpoints with expected request/response shapes
> - All automated tests pass (unit + integration)
> - Architect has reviewed architectural decisions in both codebases
> - Security has reviewed auth and data-handling paths
> - No open cross-team blockers

---

### Phase 3 — Verification & PR

**Backend**
- Create PR against {{base-branch}} (and submodule PR against {{submodule-base}} if needed)
- Ensure tests pass and SonarQube quality gate passes
- Address all CodeRabbit review comments
- PR description references {{ticket}}

**Frontend**
- Create PR against {{base-branch}}
- Ensure tests pass and SonarQube quality gate passes
- Address all CodeRabbit review comments
- PR description references {{ticket}}

---

### Coordination Rules

- **Progress tracking**: All agents update task status in tasks.md as work progresses (in-progress, completed, blocked). This is the shared progress tracker.
- **Escalation**: Unresolved disagreements escalate to the user.
- **Communication**: Agents must notify dependent agents when their outputs are ready (e.g., Backend → Frontend when endpoints are live). Don't assume — send the message.
- **Blocking issues**: Any agent can flag a blocker. Blocked agents should context-switch to unblocked work or assist the blocking agent.

### Done When

- Backend and Frontend each have a PR against {{base-branch}}
- Backend has a submodule PR against {{submodule-base}} (if applicable)
- All tests pass, SonarQube quality gates pass
- All CodeRabbit review comments addressed
- Both PRs reference {{ticket}}
```