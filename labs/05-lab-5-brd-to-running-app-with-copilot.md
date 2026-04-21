## Lab 5 - BRD to Running App with Copilot

#### Duration
16 minutes

#### Title + Learning Outcomes
**After this lab, you can:**
- move from planning artifacts to a small runnable implementation slice
- run a Spec Kit style workflow from constitution to implementation
- coordinate a 4-agent ecosystem with clear handoffs
- outline how CLI or fleet-style task execution can parallelize the next stage of delivery

#### Scenario Tie-in
Participants now turn the grievance portal backlog into a minimal working slice by following the flow from `https://github.com/AkashAi7/AI-Spec-Kit-Driven-Development`. The work uses Spec Kit phases plus a 4-agent ecosystem to move from BRD and Figma context to a runnable slice and a deployment-ready execution model.

#### Prerequisites Check
```powershell
if (-not (Test-Path .\skills\grievance-intake\SKILL.md)) { throw "Run Lab 4 first." }
"PASS: skill artifacts are available."
```

#### Sections

##### 1. Setup
1. Create a new folder named `app` in the scratch repo.
2. Clone or inspect the AI Spec Kit Driven Development repo and review its `greenfield` and `brownfield` lab guides.
3. Create a `.specify` workspace in the scratch repo or mirror the expected Spec Kit structure.
4. Use Copilot to scaffold only the smallest useful slice.

Core Spec Kit phases to use in the lab:

- `/speckit.constitution`
- `/speckit.specify`
- `/speckit.plan`
- `/speckit.tasks`
- `/speckit.implement`

Recommended ownership by phase:

| Spec Kit phase | Lead agent | Primary output |
| --- | --- | --- |
| `/speckit.constitution` | `negd-spec-planner` | project rules and constraints |
| `/speckit.specify` | `negd-spec-planner` with input from `negd-design-analyst` | feature spec |
| `/speckit.plan` | `negd-orchestrator` | phased delivery plan |
| `/speckit.tasks` | `negd-orchestrator` | task waves and owners |
| `/speckit.implement` | implementation wave directed by `negd-orchestrator` and validated by `negd-implementation-reviewer` | runnable slice |

Recommended slice:

- a single complaint submission form
- a simple category and urgency mapping rule
- a generated reference number
- a confirmation view
- one smoke test

##### 2. Hands-on Exercises
**Exercise 1**: Ask Copilot for a minimal implementation plan.

Prompt:

```text
Using BRD.md, the Figma MCP findings, artifacts/01-backlog.md, and the Spec Kit workflow, propose the smallest runnable implementation slice for the citizen grievance portal.

Return:
1. chosen stack
2. files to create
3. implementation order
4. one smoke test
5. run command
6. which agent owns each phase
```

**Exercise 2**: Generate the slice.

Task:
- Use the 4-agent ecosystem from Lab 4.
- The orchestrator should assign work in this order:
	1. `negd-design-analyst.agent.md` extracts Figma-backed UX requirements.
	2. `negd-spec-planner.agent.md` creates Spec Kit artifacts.
	3. `negd-orchestrator.agent.md` assigns the first implementation wave.
	4. `negd-implementation-reviewer.agent.md` validates the first slice.
- Ask Copilot to stop after the first runnable slice rather than building the full product.

Suggested orchestration prompts:

```text
Prompt 1 to negd-design-analyst:
Inspect the Modern Product Launch design and produce a UX mapping for a citizen grievance portal. Focus on hero, trust signals, CTA, and mobile navigation.
```

```text
Prompt 2 to negd-spec-planner:
Use BRD.md and the UX mapping handoff packet to produce Spec Kit outputs for the first MVP slice only.
```

```text
Prompt 3 to negd-orchestrator:
Create Wave 1 implementation assignments for a thin runnable slice. Limit scope to one form, one classifier, one confirmation flow, and one smoke test.
```

```text
Prompt 4 to negd-implementation-reviewer:
Review Wave 1 for design fit, accessibility, test evidence, and release readiness. Return findings in severity order.
```

**Exercise 3**: Prepare the next delivery wave.

Prompt:

```text
Create artifacts/05-delivery-wave.md with four parallel tasks for the next wave of work:
- UI hardening
- backend validation
- test expansion
- deployment automation

For each task include owner role, suggested prompt, expected files, and validation steps.

Also create artifacts/05-agent-ecosystem.md that documents:
- the four custom agents
- their responsibilities
- their inputs and outputs
- handoff order
- failure and retry conditions
```

Suggested `artifacts/05-agent-ecosystem.md` structure:

```md
# Agent Ecosystem

| Agent | Owns | Accepts | Produces | Retries when |
| --- | --- | --- | --- | --- |

## Handoff Order
1.
2.
3.
4.

## Failure Rules
-

## Escalation Rules
-
```

##### 3. Validation
- `app` contains a thin runnable slice.
- `artifacts/05-delivery-wave.md` exists.
- `artifacts/05-agent-ecosystem.md` exists.
- Participants can explain how this same plan could be executed through CLI-driven or fleet-style parallel tasking in an enterprise setup.

Validation checklist:

- The first slice is runnable locally.
- The scope is intentionally narrow rather than overbuilt.
- The next-wave task plan is decomposed into parallel work items.
- The agent ecosystem has explicit ownership and handoffs.

##### 4. Facilitator Note
- If the tenant has Copilot CLI fleet capabilities enabled, demonstrate the same task split through the CLI surface available in that environment.
- If not, use `Copilot Swarm Orchestrator` from Awesome Copilot tools as the comparison point for wave-based execution, or keep the task board artifact as the fallback explanation of the operating model.
- If participants have not used Spec Kit before, keep the lab focused on the phase model and artifact shapes, not on memorizing command syntax.

##### 5. Wrap-up
- Outcome: participants have gone from BRD to plan, to grounded context, to reusable agent patterns, to a working slice.
- This is the point where advanced GHCP features start compounding rather than feeling like disconnected demos.