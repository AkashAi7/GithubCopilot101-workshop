## Challenge 2 - Build a Public-Sector Copilot Playbook

**Goal:** Create a reusable GHCP playbook that a government delivery team can adopt across similar projects.

**Business Rationale:** Teams lose time when every engineer teaches Copilot the same rules in every conversation. A playbook makes the behavior portable and consistent.

**Scenario:** NeGD wants a baseline package for future citizen services projects so that Copilot responses consistently reflect tone, accessibility, auditability, and delivery discipline. The playbook should start from Awesome Copilot instructions and skills, then adapt them into NeGD-specific assets.

**Required outputs:**
- `.github/copilot-instructions.md`
- `artifacts/challenge-02-feature-template.md`
- `artifacts/challenge-02-review-checklist.md`
- `skills/grievance-intake/SKILL.md` updated with public-sector constraints

**Definition of Done:**
- Instructions are clear, short, and reusable.
- The feature template can be used by a developer with minimal editing.
- The review checklist includes security, accessibility, and assumption checks.
- The final assets clearly show what was adapted from Awesome Copilot and what was customized for NeGD.

**Gatekeeper Command:**
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

**Hints:**
1. **Nudge:** Keep instructions opinionated, but short enough that people will actually keep them.
2. **Targeted:** Favor formats that improve reviews: tables, checklists, explicit assumptions.
3. **Near-solution:** If the playbook cannot be reused on a second feature without rewriting it, it is too specific.