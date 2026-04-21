## Lab 1 - From Ask Mode to Structured Prompting

#### Duration
10 minutes

#### Title + Learning Outcomes
**After this lab, you can:**
- turn a BRD into epics, user stories, and acceptance criteria
- ask Copilot for structured outputs instead of broad prose
- decide when Ask mode is enough and when Agent mode adds value

#### Scenario Tie-in
Participants start with a short BRD for a citizen grievance intake portal. The goal is to produce a reviewable backlog instead of a vague summary.

#### Prerequisites Check
```powershell
$extensions = code --list-extensions
if (-not $extensions) { throw "VS Code CLI is not available in PATH." }
if ($extensions -notcontains "GitHub.copilot") { throw "GitHub Copilot extension is not installed." }
if ($extensions -notcontains "GitHub.copilot-chat") { throw "GitHub Copilot Chat extension is not installed." }
"PASS: GitHub Copilot and Chat are installed."
```

#### Sections

##### 1. Setup
1. Create a scratch folder named `citizen-service-pilot`.
2. Add a file named `BRD.md` with a short requirement set for the portal.
3. Open Copilot Chat in Ask mode.

Suggested BRD seed:

```md
# Citizen Grievance Intake Portal

The application should allow citizens to submit complaints, classify the complaint by department and urgency, generate a reference number, and allow status tracking. The first release should support web users, accessible content, and audit-friendly status updates.
```

##### 2. Hands-on Exercises
**Exercise 1**: Convert the BRD into implementation artifacts.

Prompt:

```text
Read BRD.md and produce:
1. Three epics
2. Six user stories in the format "As a..., I want..., so that..."
3. Acceptance criteria for each story
4. A short list of assumptions and open questions

Return the result as markdown with headings only for Epics, Stories, Acceptance Criteria, Assumptions, and Questions.
```

**Exercise 2**: Improve output quality with stronger constraints.

Prompt:

```text
Rewrite the backlog for a public-sector engineering team. Keep the language plain, avoid product marketing tone, include accessibility and auditability in the acceptance criteria, and prioritize the stories for a 2-week MVP.
```

**Exercise 3**: Switch to Agent mode only if needed.

Task:
- Ask Copilot to create `artifacts/01-backlog.md` from the approved backlog.
- Observe that this is a better use of Agent mode because it creates and saves an artifact rather than only answering a question.

##### 3. Validation
- `artifacts/01-backlog.md` exists.
- The file includes epics, user stories, acceptance criteria, assumptions, and open questions.
- Accessibility and auditability appear explicitly in the acceptance criteria.

Validation command:

```powershell
$content = Get-Content .\artifacts\01-backlog.md -Raw
if ($content -match 'accessib' -and $content -match 'audit') {
  'PASS: backlog includes public-sector constraints.'
} else {
  'FAIL: backlog is missing accessibility or auditability language.'
}
```

##### 4. Cleanup + Cost Teardown
- No billable resources are created.

##### 5. Next Lab Handoff
- Outcome: participants can reliably turn a BRD into actionable artifacts.
- Next: make those artifacts repeatable with custom instructions.
