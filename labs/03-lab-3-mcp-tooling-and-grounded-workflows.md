## Lab 3 - MCP Tooling and Figma-Grounded Workflows

#### Duration
12 minutes

#### Title + Learning Outcomes
**After this lab, you can:**
- explain what MCP changes in a Copilot workflow
- inspect available MCP servers and tools in VS Code
- use the Figma MCP server to pull live design context
- ask Copilot for grounded answers that use live design output rather than model-only guesses

#### Scenario Tie-in
The backlog is ready, but the team now needs answers grounded in a real design source. This lab uses the Figma MCP server against the Figma Community file `Modern Product Launch` to turn live design context into implementation guidance for the citizen grievance portal launch experience.

#### Prerequisites Check
```powershell
"Confirm in VS Code that the Figma MCP server is connected to GitHub Copilot Chat."
```

#### Sections

##### 1. Setup
1. Open the Copilot Chat tools or MCP server view in VS Code.
2. Confirm the Figma MCP server is available.
3. Use the Figma file `https://www.figma.com/community/file/1487309170684591074/modern-product-launch` as the design source.
4. Record the tool names and selected Figma frames in `artifacts/03-mcp-tool-notes.md`.

Recommended inspection order for the design walkthrough:

1. desktop landing page root frame
2. hero section with headline, primary CTA, and product visual
3. feature grid or benefits section
4. social proof or testimonial section
5. final call-to-action section
6. tablet frame
7. mobile frame and mobile navigation state

If the file exposes different frame names, keep the same order by function rather than by exact name.

##### 2. Hands-on Exercises
**Exercise 1**: Discover the Figma MCP workflow.

Task:
- Ask Copilot: "List the Figma MCP tools available to me and explain which ones I should use to inspect layout hierarchy, screenshots, and component context from the Modern Product Launch file."
- Save the response into `artifacts/03-mcp-tool-notes.md`.

Suggested prompt for the first MCP pass:

```text
Use the Figma MCP server to inspect the Modern Product Launch file.

Work in this order:
1. list top-level frames
2. identify the primary desktop landing frame
3. capture hierarchy notes for hero, feature grid, testimonial or proof area, final CTA, and mobile menu

Return a markdown table with columns:
- section
- figma evidence
- probable purpose
- reuse as-is or adapt
```

**Exercise 2**: Ground a planning task with Figma MCP.

Prompt:

```text
Using the Figma MCP server, inspect the Modern Product Launch design and create a feature implementation note for adapting it into a citizen grievance portal landing page.

Requirements:
- separate facts from assumptions
- cite which facts came from Figma tool usage
- identify the hero section, feature grid, call-to-action areas, and mobile navigation behavior
- explain which design elements can be reused directly and which need public-sector adaptation
```

Expected output shape:

```md
# Design Adaptation Note

## Tool-Derived Facts
- Fact:
- Fact:

## Assumptions
- Assumption:

## Section Mapping
| Figma section | Portal section | Reuse decision | Notes |
| --- | --- | --- | --- |

## Responsive Considerations
- Desktop:
- Tablet:
- Mobile:

## Implementation Risks
- Risk:
```

**Exercise 3**: Compare grounded and ungrounded responses.

Task:
- Ask the same question once without asking for Figma tool use.
- Compare the results and note where Figma MCP reduced guesswork about layout, hierarchy, and responsive behavior.

##### 3. Validation
- `artifacts/03-mcp-tool-notes.md` exists.
- The implementation note clearly labels tool-derived facts versus assumptions.
- Participants can explain why MCP is different from a normal prompt.

Validation checklist:

- The response references specific design sections, screenshots, or metadata returned by Figma tools.
- The response avoids fabricated UI structure or component names.
- The participant can name one case where Ask mode alone would have been weaker.

##### 4. Facilitator Note
- If the Figma MCP server supports metadata first, start there and only then use design-context or screenshot tools for specific frames.
- The objective is the decision-making pattern: discover tools, select the right one, and request evidence-backed output.
- The public Figma Community page does not guarantee stable node names in advance. For the lab, anchor participants on section function, not exact node labels.

##### 5. Next Lab Handoff
- Outcome: participants understand how MCP turns design files into live context.
- Next: package that expertise into reusable Awesome Copilot based instructions, skills, and agents.