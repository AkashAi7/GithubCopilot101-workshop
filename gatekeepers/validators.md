## Gatekeeper Validators

### Validator for Challenge 1
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

### Validator for Challenge 2
```powershell
$required = @(
  '.github/copilot-instructions.md',
  'artifacts/challenge-02-feature-template.md',
  'artifacts/challenge-02-review-checklist.md',
  'skills/grievance-intake/SKILL.md'
)
$missing = $required | Where-Object { -not (Test-Path $_) }
if ($missing.Count -eq 0) {
  'PASS: Challenge 2 artifacts are complete.'
} else {
  "FAIL: missing $($missing -join ', ')"
}
```

### Validator for Challenge 3
```powershell
$required = @(
  'artifacts/challenge-03-task-board.md',
  'artifacts/challenge-03-cli-plan.md',
  'artifacts/challenge-03-demo-notes.md',
  'artifacts/challenge-03-agent-ecosystem.md'
)
$missing = $required | Where-Object { -not (Test-Path $_) }
if ((Test-Path 'app') -and $missing.Count -eq 0) {
  'PASS: Challenge 3 artifacts are complete.'
} else {
  "FAIL: missing app folder or artifacts: $($missing -join ', ')"
}
```
