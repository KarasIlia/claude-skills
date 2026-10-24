# Systems analysis

Covers requirements engineering (elicitation, user stories, use cases, acceptance criteria, NFRs), modeling (UML, BPMN, C4, ER), API and integration design (REST/OpenAPI, async messaging), data (relational modeling, SQL), and analyst process (prioritization, traceability, working with stakeholders).

Theory notes for this domain:
- Most of it is **judgment, not syntax**, so the theory should emphasize *why* an artifact exists, who reads it, and what decisions it supports, not only its notation.
- Ground examples in one running case per topic (e.g. a food-delivery app, a bank transfer, a clinic booking system) and reuse it across sub-concepts, so the user sees how artifacts connect.
- The user is an iOS developer, so mobile-app cases and "how a developer reads this artifact" make good bridges. Point out what developers typically miss in analyst artifacts and vice versa.
- When notations or schools disagree (e.g. use cases vs user stories, BPMN purists vs pragmatists), present both and say when each fits.

## Practice workspace: a case folder of text artifacts

Everything is plain text, so it can be versioned, diffed, and reviewed:

```
~/Learning/analyst/<topic-slug>/
├── README.md
├── case/                    # input material the user works from
│   ├── brief.md             # business context, goals, constraints
│   ├── interview-*.md       # stakeholder interview transcripts, chat logs, emails
│   └── existing-spec.md     # flawed legacy docs (for "find the defect" tasks)
├── tasks/
│   └── 01-<name>.md         # task statement + space for the answer below it
└── work/                    # user's artifacts: *.md, *.mmd, openapi.yaml, schema.sql
```

Write the case material realistically: stakeholders who contradict each other, implicit assumptions, vague words ("fast", "convenient", "etc."), missing edge cases. Real input is messy, and spotting that is half the skill.

### Formats by artifact

- **Requirements, user stories, use cases, acceptance criteria:** Markdown. Gherkin (`Given / When / Then`) for acceptance criteria where it fits.
- **Diagrams (sequence, activity, state, class, ER, C4, flowcharts):** Mermaid in `.md` or `.mmd`. The user can preview them at mermaid.live, in VS Code with a Mermaid extension, in Obsidian, or on GitHub. No local renderer is installed, so don't promise one.
- **BPMN:** BPMN XML is impractical to write by hand. The user draws in a free modeler (bpmn.io demo, Camunda Modeler, or draw.io) and saves an exported PNG/SVG in `work/`. Read the image to review it. For simple flows, a Mermaid flowchart is acceptable for the warm-up.
- **API contracts:** OpenAPI 3.x YAML in `work/openapi.yaml`; AsyncAPI for event-driven topics.
- **Data modeling and SQL:** `sqlite3` is available on macOS, so SQL topics get **automatic checks**: provide `case/seed.sql` (schema + realistic data), tasks with the expected result described, and a `check.sh` that runs the user's `work/NN.sql` against a fresh database and compares the output with the expected rows. Build and run `check.sh` yourself before handing over, confirming that it fails on an empty answer and passes on your private reference solution. Then delete that solution: don't leave solutions in the folder.

### Task types for this domain

Map them to the general task mix:

- **Warm-up:** turn a short brief into a few user stories with acceptance criteria; draw a sequence diagram for a described flow.
- **Predict / explain:** "which of these requirements are testable and why?", "what will this BPMN gateway do when both conditions are true?", "what does this query return?"
- **Find the defect:** a spec with ambiguities, contradictions, missing NFRs, untestable requirements, or a diagram with notation and logic errors. Plant a known number of defects and tell the user how many, so the review is objective.
- **Build:** a use case with alternative and exception flows; an OpenAPI contract for a feature (with error responses and pagination); an ER model + DDL; a BPMN process with exceptions.
- **Elicitation role-play (great for requirements topics):** play the stakeholder. Have a hidden "true" requirements list in mind, answer only what's asked, be vague the way real stakeholders are, and contradict a colleague from another interview if the case has one. After the interview, the user writes the requirements, and review compares them against the hidden list. Keep the hidden list in your reasoning, not in a file the user can open.

## Review

There's rarely one right answer, so review against explicit criteria and name them:

- **Requirements:** ISO/IEC/IEEE 29148 quality characteristics (necessary, unambiguous, verifiable, feasible, consistent, complete, singular, traceable); INVEST for user stories; acceptance criteria that cover negative and edge cases.
- **Use cases:** a goal-level main success scenario (no UI details), complete alternative/exception flows, pre/postconditions and trigger.
- **Diagrams:** correct notation for the chosen standard, consistent level of abstraction, and agreement with the textual requirements.
- **API contracts:** resource naming, HTTP semantics and status codes, idempotency, error model, versioning, pagination, and consistency with the data model.
- **SQL / data:** run `check.sh`, then review normalization, keys/constraints, and query readability.

For defect-hunting tasks, report found / missed / false positives against the planted list.

## Sources

- **Standards and bodies of knowledge:** IIBA BABOK Guide, ISO/IEC/IEEE 29148 (requirements engineering), OMG UML and BPMN 2.0 specifications, the OpenAPI Specification (spec.openapis.org), AsyncAPI, the C4 model (c4model.com), the arc42 template, the IREB CPRE syllabus.
- **Books:** Karl Wiegers & Joy Beatty, *Software Requirements*; Alistair Cockburn, *Writing Effective Use Cases*; Mike Cohn, *User Stories Applied*; Gojko Adzic, *Specification by Example* and *Impact Mapping*; Jeff Patton, *User Story Mapping*; Martin Kleppmann, *Designing Data-Intensive Applications* (integrations and data); Bruce Silver, *BPMN Method and Style*.
- **Russian-language community:** Habr (analytics/systems analysis hubs), Analyst Days conference talks, systems.education (Denis Beskov's school of systems analysis). Verify specific links before giving them.
- **Tool docs:** Mermaid documentation (mermaid.js.org), bpmn.io, SQLite documentation.
