## Labs

This workshop assumes the audience already knows Ask mode and basic Agent mode. The lab sequence focuses on the capabilities they have not used yet: structured prompting, reusable instructions, MCP-grounded workflows, skill-driven custom agents, design-to-code with the Figma MCP server, Spec Kit driven delivery, and CLI-assisted multi-agent execution.

## Recommended flow

| Lab | Duration | Capability jump | Primary output |
| --- | --- | --- | --- |
| Lab 1 | 10 min | Move from ad hoc prompts to artifact-driven prompting | BRD backlog and acceptance criteria |
| Lab 2 | 10 min | Add custom instructions and reusable prompt patterns | Repo-scoped Copilot instructions |
| Lab 3 | 12 min | Use MCP with Figma design context | Design-grounded implementation notes |
| Lab 4 | 12 min | Install and adapt Awesome Copilot skills, instructions, and agents | Custom GHCP assets |
| Lab 5 | 16 min | Run BRD to deployment using Spec Kit and a 4-agent ecosystem | Spec artifacts, thin app slice, and orchestration plan |

## Scenario used across all labs

NeGD wants to turn a short BRD for a citizen grievance intake portal into a delivery-ready plan and then into a minimal working application slice. The experience will borrow its launch-page interaction patterns and layout inspiration from the Figma Community file `Modern Product Launch` and will be driven through Spec Kit plus a small agent ecosystem. The portal should:

- capture citizen complaints
- classify urgency and department
- generate a reference number
- show status updates
- keep prompts and outputs aligned with public-sector language and accessibility expectations

## Lab index

### Lab 1 - From Ask Mode to Structured Prompting

- Focus: turn a BRD into epics, stories, and acceptance criteria.
- Outcome: participants learn how to ask Copilot for bounded, reviewable artifacts instead of broad brainstorming.
- File: [01-lab-1-getting-started-with-github-copilot.md](./01-lab-1-getting-started-with-github-copilot.md)

### Lab 2 - Custom Instructions and Reusable Prompts

- Focus: encode team rules once so Copilot stops needing repeated steering, using Awesome Copilot instructions as the starting point.
- Outcome: participants create repo-level instructions for tone, security, accessibility, and output format.
- File: [02-lab-2-custom-instructions-and-reusable-prompts.md](./02-lab-2-custom-instructions-and-reusable-prompts.md)

### Lab 3 - MCP Tooling and Figma-Grounded Workflows

- Focus: shift from model-only answers to tool-backed answers, with the Figma MCP server as the primary design context source.
- Outcome: participants inspect the provided Figma design and turn live design context into implementation notes.
- File: [03-lab-3-mcp-tooling-and-grounded-workflows.md](./03-lab-3-mcp-tooling-and-grounded-workflows.md)

### Lab 4 - Skills and Custom Agent Design

- Focus: start from Awesome Copilot resources, then package repeatable expertise into a `SKILL.md` and custom agents.
- Outcome: participants adapt community assets into a NeGD-specific agent kit with clear boundaries and reusable instructions.
- File: [04-lab-4-skills-and-custom-agent-design.md](./04-lab-4-skills-and-custom-agent-design.md)

### Lab 5 - BRD to Running App with Copilot

- Focus: use the AI Spec Kit Driven Development flow plus a 4-agent ecosystem to move from BRD to a small runnable application slice and deployment plan.
- Outcome: participants scaffold a thin implementation, test it, and prepare a CLI-driven orchestration plan for wider delivery.
- File: [05-lab-5-brd-to-running-app-with-copilot.md](./05-lab-5-brd-to-running-app-with-copilot.md)
