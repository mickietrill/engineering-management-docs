# Task Templates

This document provides reusable templates for different types of tasks. It is split into sections based on methodology and task type.

---

## Table of Contents
- [Writing Guidelines](#writing-guidelines)
  - [Acceptance Criteria](#acceptance-criteria)
  - [Definition of Done](#definition-of-done)
  - [Priority Guidelines](#priority-guidelines)
  - [Status Definitions](#status-definitions)
  - [Assignee & Reporter Definitions](#assignee--reporter-definitions)
- [SCRUM Task Templates](#scrum-task-templates)
  - [Epic](#epic)
  - [User Story](#user-story)
  - [Technical Task](#technical-task)
    - [Frontend](#frontend)
    - [Backend](#backend)
    - [Solidity](#solidity)
    - [DevOps](#devops)
  - [Bug Report](#bug-report)
  - [Sub-task](#sub-task)
  - [QA Checklist](#qa-checklist)
  - [Spike / Research Task](#spike--research-task)
  - [Docs](#docs)

---

# Writing Guidelines
To ensure consistency, clarity, and traceability across all task types, this section defines **universal standards** for writing key fields like `Acceptance Criteria` and `Definition of Done`. These can be referenced in any task template.

## Acceptance Criteria
Acceptance Criteria define **measurable, clear, and testable conditions** that must be fulfilled for a task to be considered complete.
> *(Required in most tasks)*

### Best Practices
- Use bullet points for clarity.
- Use **Gherkin-style** format (`Given / When / Then`) for logic-based functionality.
- Avoid ambiguity — make the criteria as specific and objective as possible.
- Should reflect **user perspective** and **business expectations**.

### Example (General Bullet Format)
```md
- User can upload a file up to 100MB
- Errors are shown for unsupported formats
- Upload progress indicator is visible
```

### Example (Gherkin Format)
```gherkin
Given I am logged in
When I navigate to the Upload screen
Then I should be able to upload a valid image
```

## Definition of Done
Definition of Done (DoD) outlines the **internal quality and completion checklist** that a task must fulfill before it can be moved to `Done`.
> *(Optional but Recommended)*

> Note: DoD is typically more technical and delivery-oriented than Acceptance Criteria.

### Best Practices
- Focus on delivery quality: testing, review, documentation, deployment.
- Tailor per domain: e.g., frontend, backend, Solidity, DevOps.
- Use checkboxes or bullet points.

### Example (General)
```md
- [x] Code implemented and pushed
- [x] Tests added and passed
- [x] QA verified
- [x] Documentation updated
```

### Example (Solidity Task)
```md
- [x] Contract compiled without errors
- [x] Unit and integration tests cover main logic
- [x] Testnet deployment verified
- [x] Code reviewed for security patterns (reentrancy, overflow, etc.)
```

## When to Use
| Section              | Task Types                | Required |
|----------------------|---------------------------|-------|
| **Acceptance Criteria** | Epics, Stories, Bugs, Research | Yes   |
| **Definition of Done**  | Tech Tasks, Subtasks, QA, DevOps | Yes   |

## Tips for Better Writing
- Keep it **short**, **clear**, and **actionable**.
- Collaborate with stakeholders or QA to validate criteria.
- Avoid technical jargon unless needed.
- Update the criteria if task scope changes.

## Priority Guidelines
Choosing the correct priority helps the team triage and organize work efficiently.

| Priority      | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| **Highest**   | Critical production issues, security vulnerabilities, or blocking releases |
| **High**      | Tasks required for upcoming release or sprint-critical                     |
| **Medium**    | Valuable but not urgent tasks                                              |
| **Low**       | Nice-to-have improvements, non-blocking enhancements                      |

> When in doubt, align with your product manager or tech lead.

## Status Definitions
Track and reflect task progress clearly with consistent status usage.

| Status          | Description                                                           |
|------------------|-------------------------------------------------------------------------|
| **To Do**        | Task is approved and ready to be picked up                            |
| **In Progress**  | Task is currently being worked on                                     |
| **In Review**    | Task is under code review or waiting for testing                      |
| **Blocked**      | Task cannot proceed due to external dependencies                      |
| **Done**         | Task is complete, merged, tested and deployed                         |

> Use "Blocked" actively to highlight issues early.

## Assignee & Reporter Definitions
Clarify responsibilities and improve task ownership with consistent usage of metadata fields.

| Field         | Description                                                                  |
|---------------|------------------------------------------------------------------------------|
| **Assignee**  | Person who is **responsible for completing the task**. Usually a developer, QA, or designer. |
| **Reporter**  | Person who **created or assigned** the task. Typically a product owner, team lead, or stakeholder. |

> Ensure every task has both fields filled to maintain clarity on ownership and origin.


---

# SCRUM Task Templates
Templates tailored for Scrum methodology. Use them in any task tracker (Jira, Notion, GitHub Issues, etc.).

Each task should include:
- Clear title (e.g., [Component/Module] – [Task Type] – [Action])
- Description with purpose, outcome, references
- Acceptance Criteria
- Dependencies, Epic links, tags, and deadlines
- Section for the assignee to document **Result** after task is completed

## Epic
> An **Epic** is a large body of work that can be broken down into multiple user stories or tasks. Use this template to define major features or initiatives and align stakeholders on the scope and value of the work.

## Epic Summary or Title *(Required)*
Provide a concise title that reflects the broader functionality or theme.
> Format: [Component/Module] – Epic – [Action]

## Description *(Required)*
- **Context:** [Business background or technical motivation]
- **Objective:** [What needs to be achieved]
- **Value:** [What value this brings to users or business]
- **References:** [Links to docs, mockups, or related materials]

## Breakdown *(Required)*
List the associated User Stories or Tasks that are part of this Epic.
- TS-101 – [Task title]
- TS-102 – [Task title]
- TS-103 – [Task title]

(Use real issue/story IDs when linking in Jira or task tracker.)

## Linked Issues *(Optional)*
- Blocks: [List of dependent issues]
- Is Blocked By: [Other epics or system dependencies]

## Epic Metadata
- **Task ID:** [EPIC-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result (To be filled upon completion)
- Summary of completed work
- [Link to PR or commit]
- [Link to documentation or release notes]
- Test summary or outcome and coverage report

## User Story
> A **User Story** represents a specific, actionable requirement from the perspective of the end user. Use this template to describe a unit of functionality that delivers value to users and can be implemented within a sprint.

## Story Summary or Title *(Required)*
Provide a clear and concise title that captures the feature or enhancement.
> Format: [Component/Module] – User Story – [Action]

## Description *(Required)*
Explain the context and purpose of this story. Clearly describe what the user should be able to do and why it matters. Reference any design files, documentation, or research that may help with implementation.

## Linked Issues *(Optional)*
- Related Epic: EPIC-XXX
- Blocks: [Other stories or tasks]
- Is Blocked By: [Dependencies]

## User Story Metadata
- **Task ID:** [USERSTORY-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result (To be filled upon completion)
- Summary of completed work
- [Link to PR or commit]
- [Link to documentation or release notes]
- Test summary or outcome and coverage report

---

## Technical Task
> A **Technical Task** is used to describe a concrete, technical implementation step, not directly visible to end users but required to support user stories, epics, or technical infrastructure.

### Frontend
This template is focused on frontend implementation.

## Task Summary or Title *(Required)*
Provide a concise and clear task name that quickly communicates the core of the work to be done.
> Format: [Component/Module] – Frontend – [Action]

## Description *(Required)*
Provide a brief explanation of what needs to be implemented and why. This section should:
- Describe the purpose of the task from a technical standpoint.
- Clarify the scope (what's included or excluded).
- Mention relevant components, design systems, or frontend frameworks to be used.
- Link to any visual references (e.g., mockups or wireframes).

## Requirements *(Required)*
List the technical requirements or subtasks clearly. This could include:
- UI elements to be developed or changed.
- User interactions and behaviors.
- External dependencies (e.g., API endpoints).
- Accessibility or responsiveness constraints.
  Use bullet points for clarity.

## Linked Issues *(Optional)*
Link related tasks such as:
- Associated User Story
- Epic
- Backend or DevOps tasks
- Use JIRA IDs or GitHub issue links as appropriate.

## Task Metadata
- **Task ID:** [FRONTEND-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work
- [Link to PR or commit]
- [Link to documentation or release notes]
- [Link to deployed functionality]
- Test summary or outcome and coverage report

### Backend
> A **Technical Task** is used to describe a backend-related implementation or improvement required to support business logic, APIs, or infrastructure integration.

## Task Summary or Title *(Required)*
Provide a concise and descriptive name for the task.

> Format: [Component/Module] – Backend – [Action]

## Description *(Required)*
Describe what the backend task is about and its purpose. This should include:
- Business or technical context for the task
- Scope and focus (e.g., API creation, database change, logic improvement)
- Technologies or systems involved (e.g., Node.js, PostgreSQL, message broker)
- References to documentation or related diagrams

## Requirements *(Required)*
List all technical deliverables expected from the task. For example:
- Add new REST/GraphQL endpoint
- Update database schema
- Implement background job
- Ensure error handling and logging
- Update unit/integration tests

## Linked Issues *(Optional)*
Reference related tickets:
- Linked Epic or User Story
- Dependent frontend or DevOps task
- Blocking or blocked tasks

## Task Metadata
- **Task ID:** [BACKEND-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work
- [Link to PR or commit]
- [Link to documentation or release notes]
- [Link to deployed functionality]
- Test summary or outcome and coverage report

### Solidity
> A **Technical Task** for Solidity describes the implementation or update of smart contracts, related libraries, or blockchain-specific logic.

## Task Summary or Title *(Required)*
Give the task a short and descriptive title.
> Format: [Component/Module] – Solidity – [Action]

## Description *(Required)*
Briefly explain what should be done and why. Include:
- Context or motivation (e.g., feature request, refactor, vulnerability patch)
- Scope of the task (what the contract/module should do)
- Related standards or protocols (e.g., ERC-20, ERC-721, OpenZeppelin)
- Links to diagrams, specs, or whitepapers if applicable

## Requirements *(Required)*
Clearly outline the implementation expectations:
- Write or modify specific functions
- Apply gas optimization or pattern improvements
- Follow specific access control models
- Ensure events are properly emitted
- Write test cases for new logic

## Linked Issues *(Optional)*
Add any related:
- Epics or User Stories
- Frontend or backend integrations
- Security audit tickets

## Task Metadata
- **Task ID:** [SOLIDITY-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work
- [Link to PR or commit]
- [Link to documentation or release notes]
- [Link to deployed functionality]
- Test summary or outcome and coverage report

### Devops
> A **DevOps Task** documents infrastructure, deployment, CI/CD, monitoring, or configuration-related work.

## Task Summary or Title *(Required)*
Use a short, descriptive name that reflects the infrastructure change.
> Format: [Component/Module] – Devops – [Action]
> 
## Description *(Required)*
Clearly describe the objective of the task:
- What needs to be created, modified, or removed
- Motivation: performance, security, automation, cost optimization, etc.
- Affected services or environments
- Risks or impact of the changes
- Include diagrams or architecture links if applicable

## Requirements *(Required)*
Define what should be achieved:
- Infrastructure setup or configuration
- CI/CD pipelines
- Monitoring/alerting
- Access control or secrets management
- Rollback plan or testing environment setup

## Linked Issues *(Optional)*
- Related epic, feature, or bug
- Security audit tasks
- Linked to deployment task or external vendor

## Task Metadata
- **Task ID:** [DEVOPS-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work [Monitoring results, Link to pipeline... ]
- [Link to PR or commit]
- [Link to documentation or release notes]
- [Link to deployed functionality]
- Test summary or outcome and coverage report

## Bug Report
> A **Bug Task** is used to report and track defects, regressions, or unexpected behavior in the system.

## Task Summary or Title *(Required)*
Provide a clear and short name describing the bug.
> Format: [Component/Module] – Bug – [Action]

## Description *(Required)*
Describe the issue in detail:
- Where and when it was discovered
- Expected behavior vs actual behavior
- Steps to reproduce the bug (if applicable)
- Screenshots or logs (if available)
- Environment info (device, OS, browser, network, chain)

## Severity *(Required)*
Define business impact:
- **Blocker** – No progress can be made
- **Critical** – Major impact on functionality or data
- **Major** – Serious issue, but with workarounds
- **Minor** – Doesn't affect core functionality
- **Trivial** – UI/UX or cosmetic issue

## Requirements *(Required)*
List what needs to be fixed:
- What component/feature needs change
- What outcome should be verified after the fix
- Any regression checks if needed

## Linked Issues *(Optional)*
- Related User Story or Epic
- Other bugs or features that are impacted

## Task Metadata
- **Task ID:** [BUG-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work
- [Link to PR or commit]
- [Link to documentation or release notes]
- [Link to deployed functionality]
- Test summary or outcome and coverage report

## Sub-task
> A **Sub-task** is a small, clearly scoped part of a larger task (such as a Story, Bug, or Technical Task). Sub-tasks help break down work into manageable units and improve tracking.

## Summary or Title *(Required)*
Use a clear and specific title. 
> Format: [Parent Feature] - [Component/Module] – Sub-task – [Action]

## Description *(Required)*
Briefly describe:
- What exactly should be done
- How it relates to the parent task
- Any dependencies or blockers
- Relevant links or designs (if any)

Keep it focused — a sub-task should represent one concrete action or step.

## Task Metadata
- **Task ID:** [SUBTASK-XXX]
- **Parent Task:** [Link or ID of Story/Bug/Task]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work
- [Link to PR or commit]
- [Link to documentation or release notes]
- [Link to deployed functionality]
- Test summary or outcome and coverage report

## QA Checklist
> A **QA Checklist** is used to ensure thorough testing of a feature, bug fix, or release before it's accepted into production.

## Task Summary or Title *(Required)*
Clearly state what is being tested.
> Format: [Component/Module] – QA – [Action]

## Description *(Required)*
Briefly describe:
- What should be tested
- Context of the task (linked to story/bug)
- Type of testing required (manual, regression, e2e, cross-browser, etc.)
- Any environment-specific notes (e.g., works only on testnet)

## Requirements *(Optional)*
- Browsers/devices to test
- Wallets or user flows to cover
- Test data or setup instructions
- Feature toggles or special conditions
- Localization, accessibility, or responsiveness requirements

## QA Checklist *(Required)*
> Check each item after completion. Add or remove items depending on the feature.
- [ ] Feature works as expected based on acceptance criteria
- [ ] Negative cases are handled correctly (invalid inputs, edge cases)
- [ ] UI is aligned with designs (spacing, colors, responsiveness)
- [ ] Errors are displayed and logged properly
- [ ] No regression in related functionality
- [ ] API responses and performance acceptable
- [ ] Compatible on all target devices/browsers
- [ ] Wallet/connect flow works correctly
- [ ] Blockchain interaction successful (if applicable)
- [ ] Localizations tested (if multilingual)
- [ ] Security/privacy checks completed (no sensitive data leakage)

## Task Metadata
- **Task ID:** [QA-XXX]
- **Assignee:** [Name]
- **Linked to:** User Story / Bug / Epic
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work [Passed scenarios, Failed scenarios]
- [Link to PR or commit]
- [Link to documentation or release notes]
- [Link to deployed functionality]
- Test summary or outcome and coverage report

## Spike / Research Task
> A **Research Task** is created when the team needs to explore a new technology, tool, architectural decision, or business requirement before implementation. The goal is to gather insights, compare options, and reduce uncertainty.

## Task Summary or Title *(Required)*
Use a clear and concise title. 
> Format: [Component/Module] – Research – [Action]

## Description *(Required)*
Provide context and clarify:
- What needs to be researched?
- What problem or opportunity are we addressing?
- Why is this research important?
- What is the expected depth (exploratory overview or deep investigation)?

## Research Requirements / Scope *(Required)*
Define the boundaries and expectations:
- Key questions to answer
- Criteria to evaluate potential solutions
- Technologies, frameworks, or approaches to compare
- Constraints, limitations, or blockers to consider

## Deliverables *(Required)*
Clearly state what should be delivered:
- Comparison table (pros/cons, cost, performance, complexity)
- Summary report or recommendation
- Link to documentation or knowledge base
- Visuals (architecture diagram, flowchart, PoC)
- Suggested next steps

Specify format and storage:
- Google Doc, Confluence, Notion, GitHub Wiki, etc.

## Task Metadata
- **Task ID:** [SPIKE-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work [Recommended solution, Supporting links, Table or matrix]
- [Link to PR or commit]
- [Link to documentation or release notes]
- Test summary or outcome and coverage report

## Docs
> A **Docs Task** is used when a documentation-related deliverable needs to be created, updated, reviewed, or restructured. It may cover internal processes, user-facing documentation, or developer resources.

## Summary or Title *(Required)*
Use a clear, action-oriented title. 
> Format: [Component/Module] – Docs – [Action]

## Description *(Required)*
Describe the documentation need:
- What should be created or changed?
- Who is the target audience (e.g. developers, end users, internal teams)?
- Why is this documentation important now (e.g. after a new feature, refactor, or customer feedback)?
- Where will the documentation live (e.g. GitHub, Confluence, Notion)?

Include:
- Existing links to documentation or related specs
- Visual assets or diagrams (if needed)
- Requirements for formatting or localization

## Structure/Scope *(Optional but Recommended)*
Outline the structure or key sections to include:
- Overview
- Setup instructions
- Usage examples
- FAQs / Troubleshooting

## Task Metadata
- **Task ID:** [DOCS-XXX]
- **Assignee:** [Name]
- **Reporter:** [Name]
- **Priority:** High / Medium / Low
- **Status:** To Do / In Progress / Done
- **Labels / Tags:** [e.g., frontend, bug, research]

## Result *(To be filled upon completion)*
- Summary of completed work
- [Link to PR or commit]
- [Link to documentation or release notes]
- Test summary or outcome and coverage report
