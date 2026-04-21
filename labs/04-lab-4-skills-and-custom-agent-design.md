## Lab 4 - Skills and Custom Agent Design

#### Duration
12 minutes

#### Title + Learning Outcomes
**After this lab, you can:**
- describe when a `SKILL.md` is useful
- create a skill that narrows Copilot to a repeatable engineering task
- define a custom agent persona with scope, boundaries, and expected outputs

#### Scenario Tie-in
The team wants a repeatable grievance-intake assistant that can translate new BRDs and Figma-driven UX context into implementation-ready artifacts without re-teaching Copilot every time.

This lab starts from Awesome GitHub Copilot resources instead of writing everything from scratch.

#### Prerequisites Check
```powershell
if (-not (Test-Path .\artifacts\03-mcp-tool-notes.md)) { throw "Run Lab 3 first." }
"PASS: MCP discovery notes are available."
```

#### Sections

##### 1. Setup
Create the folders `skills/grievance-intake` and `prompts` in the scratch repo.

Reference sources:

- `https://awesome-copilot.github.com/skills/`
- `https://awesome-copilot.github.com/instructions/`
- `https://awesome-copilot.github.com/agents/`
- `https://awesome-copilot.github.com/tools/`

Suggested assets to inspect before drafting:

- Instruction patterns: `agent-skills`, `agents`, `a11y`, `agent-safety`
- Skill patterns: `copilot-instructions-blueprint-generator`, `prompt-builder`, `suggest-awesome-github-copilot-skills`
- Agent patterns: `specification`, `implementation-plan`, `gem-designer`, `gem-reviewer`, `gem-orchestrator`
- Tooling references: `Awesome Copilot MCP Server`, `Awesome GitHub Copilot Browser`, `Copilot Swarm Orchestrator`

##### 2. Hands-on Exercises
**Exercise 1**: Derive a NeGD skill from Awesome Copilot references.

Prompt:

```text
Create skills/grievance-intake/SKILL.md for a Copilot skill that helps with a public-sector citizen grievance portal.

The skill should:
- read a BRD
- read design context from the Figma MCP server
- extract scope, actors, workflows, and risks
- produce backlog items and validation steps
- remind the user to separate verified facts from assumptions
- avoid inventing compliance claims or external dependencies
- include a short frontmatter or header note naming which Awesome Copilot skill patterns influenced the file
```

**Exercise 2**: Create a 4-agent ecosystem.

Prompt:

```text
Create four custom agent files in prompts/agents using Awesome Copilot agent patterns as references:

1. negd-orchestrator.agent.md
2. negd-design-analyst.agent.md
3. negd-spec-planner.agent.md
4. negd-implementation-reviewer.agent.md

Rules:
- The orchestrator delegates work and owns handoff order.
- The design analyst uses Figma MCP context.
- The spec planner aligns work to Spec Kit phases.
- The implementation reviewer checks accessibility, security, and delivery readiness.
- Each file must include purpose, triggers, inputs, outputs, stop conditions, and handoff contract.
```

Use these concrete agent roles:

| Agent | Primary responsibility | Input packet | Output packet | Hands off to |
| --- | --- | --- | --- | --- |
| `negd-orchestrator` | Decide sequence, assign waves, track status | BRD, design note, constraints | work plan, assignments, risks | design analyst or spec planner |
| `negd-design-analyst` | Translate Figma evidence into implementable UX notes | Figma file, selected frames, portal goal | UX mapping, component list, adaptation risks | spec planner |
| `negd-spec-planner` | Convert BRD and UX notes into Spec Kit artifacts | BRD, UX mapping, repo instructions | constitution, spec, plan, tasks | orchestrator |
| `negd-implementation-reviewer` | Validate slice quality and readiness | changed files, test results, design rules | findings, release decision, follow-up tasks | orchestrator |

Starter prompt for `negd-orchestrator.agent.md`:

```text
You are the NeGD delivery orchestrator.

Your job is to route work across three specialist agents and keep outputs narrow.
Always gather the minimum context needed, decide the next owner, and emit a handoff packet.
Never implement UI details yourself when design context is missing.
Never approve a delivery wave without validation evidence.

Return sections in this order:
1. objective
2. current evidence
3. next agent
4. handoff packet
5. completion criteria
```

Starter prompt for `negd-design-analyst.agent.md`:

```text
You are the NeGD design analyst.

Use the Figma MCP server to inspect the selected design frames.
Extract only observable layout, hierarchy, navigation, and component facts.
Separate evidence from interpretation.
Map commercial landing-page patterns to public-sector service patterns.

Return sections in this order:
1. figma evidence
2. reusable patterns
3. required adaptations
4. ux risks
5. handoff packet for spec planner
```

Starter prompt for `negd-spec-planner.agent.md`:

```text
You are the NeGD spec planner.

Convert BRD input and design evidence into Spec Kit style artifacts.
Produce outputs aligned to constitution, specification, plan, and tasks.
Favor MVP scope, public-sector wording, auditability, and accessibility.

Return sections in this order:
1. constitution deltas
2. specification summary
3. implementation plan
4. task waves
5. handoff packet for orchestrator
```

Starter prompt for `negd-implementation-reviewer.agent.md`:

```text
You are the NeGD implementation reviewer.

Review the first runnable slice against accessibility, public-sector language, design fidelity, test evidence, and deployment readiness.
Do not rewrite the whole implementation. Return findings, residual risk, and go or no-go guidance.

Return sections in this order:
1. findings
2. evidence reviewed
3. go-no-go decision
4. required fixes
5. handoff packet for orchestrator
```

Use this handoff packet template in every agent file:

```md
## Handoff Packet
- From:
- To:
- Objective:
- Inputs received:
- Artifacts produced:
- Open questions:
- Exit criteria for next agent:
```

Use this minimum output schema in every agent file:

```yaml
agent_name:
mode:
objective:
inputs:
artifacts:
risks:
open_questions:
next_agent:
completion_state:
```

**Exercise 3**: Evaluate the design.

Task:
- Ask Copilot to run through one example request: "Turn BRD.md and the Modern Product Launch Figma file into an MVP delivery plan."
- Save the output in `artifacts/04-agent-dry-run.md`.

Suggested dry-run sequence:

1. run `negd-design-analyst` on the hero and mobile frames
2. pass the handoff packet to `negd-spec-planner`
3. ask `negd-orchestrator` to define wave 1
4. ask `negd-implementation-reviewer` what evidence will be needed before sign-off

##### 3. Validation
- `skills/grievance-intake/SKILL.md` exists.
- `prompts/agents` contains four custom agent files.
- `artifacts/04-agent-dry-run.md` exists and contains scope, tasks, validation, and risks.
- Every agent file includes both a handoff packet template and an output schema.

Validation command:

```powershell
$required = @(
  'skills/grievance-intake/SKILL.md',
  'prompts/agents/negd-orchestrator.agent.md',
  'prompts/agents/negd-design-analyst.agent.md',
  'prompts/agents/negd-spec-planner.agent.md',
  'prompts/agents/negd-implementation-reviewer.agent.md',
  'artifacts/04-agent-dry-run.md'
)
$missing = $required | Where-Object { -not (Test-Path $_) }
if ($missing.Count -eq 0) {
  'PASS: skill, four-agent ecosystem, and dry run output are present.'
} else {
  "FAIL: missing $($missing -join ', ')"
}
```

##### 4. Cleanup + Cost Teardown
- No billable resources are created.

##### 5. Next Lab Handoff
- Outcome: the team has a reusable GHCP asset pack grounded in community patterns.
- Next: run the BRD through Spec Kit and orchestrate the 4-agent ecosystem into a thin running slice.