## Challenge 1 - Create a Custom MCP Agent

**Goal:** Design a custom GHCP 4-agent kit for the citizen grievance portal that uses MCP tools when live context is available.

**Business Rationale:** The team wants more than generic chat help. They need a small set of cooperating agents that can turn a BRD and design context into grounded delivery outputs with less manual steering.

**Scenario:** A product owner drops a new BRD into the repo and asks for an MVP delivery plan. The agent kit should inspect available context, use MCP tools where appropriate, and return a concise implementation package. The kit should borrow structure and wording patterns from Awesome Copilot skills, instructions, and agent files instead of being authored from scratch.

**Required outputs:**
- `skills/grievance-intake/SKILL.md`
- `prompts/agents/negd-orchestrator.agent.md`
- `prompts/agents/negd-design-analyst.agent.md`
- `prompts/agents/negd-spec-planner.agent.md`
- `prompts/agents/negd-implementation-reviewer.agent.md`
- `artifacts/challenge-01-agent-output.md`

**Definition of Done:**
- The skill defines scope, inputs, outputs, and boundaries.
- The four agent files explain when each agent should use MCP tools or hand off work.
- The dry-run output includes facts, assumptions, tasks, and validation steps.

**Gatekeeper Command:**
```powershell
$required = @(
	'skills/grievance-intake/SKILL.md',
	'prompts/agents/negd-orchestrator.agent.md',
	'prompts/agents/negd-design-analyst.agent.md',
	'prompts/agents/negd-spec-planner.agent.md',
	'prompts/agents/negd-implementation-reviewer.agent.md',
	'artifacts/challenge-01-agent-output.md'
)
$missing = $required | Where-Object { -not (Test-Path $_) }
if ($missing.Count -eq 0) {
	'PASS: Challenge 1 artifacts are complete.'
} else {
	"FAIL: missing $($missing -join ', ')"
}
```

**Hints:**
1. **Nudge:** Separate what the agent knows from what it must verify with tools.
2. **Targeted:** Make every agent contract narrow: purpose, inputs, outputs, stop conditions, handoff.
3. **Near-solution:** If you cannot explain why one agent exists separately from another, the ecosystem is still too generic.
