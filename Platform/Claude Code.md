## Global Config (CLAUDE.md)

### Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it via subagents
- One task per subagent for focused execution

## Agent Team Sample
```
i need to work on [feature-name]. Create an agent team to implement the required changes. Spawn the following members

Planner - gather and compile the requirements using this XXX and all its subtasks/child issues then run XXX → discuss with team → finalize the plan → XXX → XXX → XXX to validate consistency before implementation begins

Architect - use senior-architect skill, to help Planner and Backend to finalize the plan

Security - use senior-security skill, to help Architect and Backend to identify any security issues

Frontend - use senior-frontend skill, to work in XXX repo [repo-path] using worktree [worktree-name] branch off from staging, work closely with Backend when the backend changes are ready, report any backend issues or request to backend. During planning phase, review API contracts from Architect and start component scaffolding.

Backend - use senior-backend skill, to work in [repo-name] repo [repo-path] using worktree [worktree-name] branch off from staging, and its submodule branch off from master, work closely with Security for backend changes. When the changes are ready, inform Frontend and fix issues or address request requested by Frontend. Utilize [gen-test-kill] skill to generate/update tests for the new changes

Unresolved disagreements escalate to the user.

All agents: Update task status in tasks.md as work progresses (mark in-progress, completed, or blocked). This is the shared progress tracker.

Done when: Backend and Frontend each have a PR created against staging (and Backend creates a submodule PR against master if submodule changes are needed) with tests and sonarqube quality gate passing. Both PRs reference the XXX and address all CodeRabbit review comments.
```