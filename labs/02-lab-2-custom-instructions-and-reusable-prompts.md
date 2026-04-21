## Lab 2 - Custom Instructions and Reusable Prompts

#### Duration
10 minutes

#### Title + Learning Outcomes
**After this lab, you can:**
- create repo-level custom instructions for GitHub Copilot
- reduce repetitive steering in prompts
- standardize public-sector tone, security, and accessibility expectations

#### Scenario Tie-in
The team has a decent backlog from Lab 1, but every prompt still has to restate tone, compliance expectations, and output format. This lab fixes that.

Use Awesome Copilot as the source catalog for reusable instruction patterns. Participants should browse the `Instructions` section first and adapt, not invent from scratch.

#### Prerequisites Check
```powershell
if (-not (Test-Path .\artifacts\01-backlog.md)) { throw "Run Lab 1 first." }
"PASS: Lab 1 backlog artifact is available."
```

#### Sections

##### 1. Setup
Create the folder `.github` in the scratch repo if it does not exist.

Reference sources:

- `https://awesome-copilot.github.com/instructions/`
- Suggested starting points to browse: `a11y`, `agent-safety`, `context-engineering`, `security-and-owasp`, and `spec-driven-workflow-v1`

##### 2. Hands-on Exercises
**Exercise 1**: Ask Copilot to draft repo instructions from Awesome Copilot references.

Prompt:

```text
Using patterns from Awesome Copilot instructions, create a .github/copilot-instructions.md file for a public-sector citizen services project.

Requirements:
- Use plain and formal language.
- Prefer accessible UX and clear status messaging.
- Include auditability and traceability in backend and workflow suggestions.
- Favor small, reviewable pull requests.
- When generating output, prefer markdown tables for plans and checklists for validation.
- Do not invent APIs or tools when context is missing.
- Add a short "Source inspirations" section listing which Awesome Copilot instructions influenced the final file.
```

**Exercise 2**: Create a reusable prompt template.

Prompt:

```text
Using the repo instructions, create artifacts/02-feature-prompt-template.md.
The template should help a developer ask Copilot for:
1. a feature summary
2. implementation steps
3. test cases
4. risks and assumptions
```

**Exercise 3**: Test the instructions.

Task:
- Ask Copilot to produce a solution outline for the complaint submission feature.
- Verify that the response follows the tone and structure without re-stating the rules.
- Verify that the final instructions are adapted to NeGD rather than copied verbatim from the catalog.

##### 3. Validation
- `.github/copilot-instructions.md` exists.
- `artifacts/02-feature-prompt-template.md` exists.
- A generated response now includes accessibility, auditability, and implementation/test sections without the user repeating those requirements.

Validation command:

```powershell
$required = @(
  '.github/copilot-instructions.md',
  'artifacts/02-feature-prompt-template.md'
)
$missing = $required | Where-Object { -not (Test-Path $_) }
if ($missing.Count -eq 0) {
  'PASS: custom instructions and prompt template are present.'
} else {
  "FAIL: missing $($missing -join ', ')"
}
```

##### 4. Cleanup + Cost Teardown
- No billable resources are created.

##### 5. Next Lab Handoff
- Outcome: the team can encode working norms once instead of repeating them in every chat.
- Next: connect Copilot to live tools through MCP.