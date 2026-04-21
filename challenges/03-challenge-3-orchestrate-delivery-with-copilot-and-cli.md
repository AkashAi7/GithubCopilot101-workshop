## Challenge 3 - Orchestrate Delivery with Copilot and CLI

**Goal:** Turn the BRD into a thin implementation slice and prepare a CLI-driven, fleet-style task execution plan using Spec Kit and a 4-agent ecosystem for the next delivery wave.

**Business Rationale:** The customer has used Ask mode and Agent mode, but not GHCP as an execution system. This challenge introduces decomposition, parallel work, and operating at team scale.

**Scenario:** The first MVP slice is approved. Now the team needs to split follow-on work so multiple contributors or agent tasks can run in parallel with clear prompts and validation steps. The work must use the Figma-backed design context, the Spec Kit phase model, and four custom agents that function together rather than as isolated personas.

**Required outputs:**
- `app/` with a minimal runnable slice
- `artifacts/challenge-03-task-board.md`
- `artifacts/challenge-03-cli-plan.md`
- `artifacts/challenge-03-demo-notes.md`
- `artifacts/challenge-03-agent-ecosystem.md`

**Required agent contracts:**
- `prompts/agents/negd-orchestrator.agent.md`
- `prompts/agents/negd-design-analyst.agent.md`
- `prompts/agents/negd-spec-planner.agent.md`
- `prompts/agents/negd-implementation-reviewer.agent.md`

**Definition of Done:**
- The app slice handles complaint submission at a basic level.
- The task board splits the next work into at least three parallel tracks.
- The CLI plan explains how the team would run those tasks through the CLI or a fleet-enabled environment.
- The agent ecosystem defines four agents, their contracts, and their handoff order.
- Each agent contract includes a starter prompt, a handoff packet, and an output schema.
- Demo notes explain what was built, what remains, and how GHCP accelerated delivery.

**Gatekeeper Command:**
```powershell
$required = @(
  'artifacts/challenge-03-task-board.md',
  'artifacts/challenge-03-cli-plan.md',
  'artifacts/challenge-03-demo-notes.md',
  'artifacts/challenge-03-agent-ecosystem.md',
  'prompts/agents/negd-orchestrator.agent.md',
  'prompts/agents/negd-design-analyst.agent.md',
  'prompts/agents/negd-spec-planner.agent.md',
  'prompts/agents/negd-implementation-reviewer.agent.md'
)
$missing = $required | Where-Object { -not (Test-Path $_) }
if ((Test-Path 'app') -and $missing.Count -eq 0) {
  'PASS: Challenge 3 artifacts are complete.'
} else {
  "FAIL: missing app folder, agent contracts, or artifacts: $($missing -join ', ')"
}
```

**Hints:**
1. **Nudge:** Keep the first implementation slice deliberately small.
2. **Targeted:** A good task board includes prompt, owner role, output files, validation, and agent assignment for each task.
3. **Near-solution:** If your CLI plan is just a list of commands with no task decomposition or handoff model, you have not shown fleet-style thinking yet.

**Suggested task-board schema:**

```md
| Wave | Task | Agent | Prompt seed | Expected artifacts | Validation |
| --- | --- | --- | --- | --- | --- |
```

**Suggested CLI-plan schema:**

```md
# CLI Plan

## Preconditions
-

## Wave 1
- Agent:
- Goal:
- Command or CLI surface:
- Expected evidence:

## Wave 2
-

## Merge Gate
-
```