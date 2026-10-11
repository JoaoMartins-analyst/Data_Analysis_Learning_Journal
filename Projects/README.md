# Projects

Each project needs a question, source/data permission record, reproducible work, validation, findings and honest limits.

| Project | Purpose | Imported status |
|---|---|---|
| [P1 Trail & Tide](p1-trail-and-tide/README.md) | Finish the existing Excel/MySQL foundation project | In progress |
| [P1B Power BI extension](p1b-power-bi-extension/README.md) | Extend P1 with preparation, modelling and a decision report | Not started |
| [Phase 2 analysis utility](analysis-utility/README.md) | Trusted Python/pandas calculation layer | Not started |
| [PA1 unattended assistant](pa1-unattended-analysis-assistant/README.md) | Real API/tool/scheduling extension of that utility | Not started |
| [Restaurant pilot](restaurant-pilot/README.md) | One owner, one question, bounded free delivery and feedback | Discovery in progress |

P2A–P2D are the later Restaurant Data Platform stages. P3 is optional advanced AI work; see [later progression](../Later/README.md). The Phase 2 utility is not renamed P2, because P2 already identifies the engineering project in the workbook.

## Suggested layout inside a project

Add folders only when there is real work to save:

| Path | Use |
|---|---|
| README.md | Question, status, outputs, reproduction and evidence links |
| data/public-or-synthetic/ | Shareable fixtures with source/licence and date |
| sql/ | Queries, schema and SQL checks |
| code/ | Actual implementation |
| tests/ | Cases and checks |
| outputs/ | Checked reports, charts and static previews |
| evidence/ | QA, reconciliation, assessment links and redacted execution records |

Keep private client inputs and raw logs outside the public repository. A client authorising analysis does not automatically authorise GitHub publication or upload to an AI provider. Publish a synthetic recreation or material explicitly approved for publication.

Use the [project brief](../Templates/project-brief.md) and [QA log](../Templates/qa-log.md). If a project already has its own repository or established folder, link to it here instead of maintaining two copies.

This pack contains READMEs and templates. It does not include the learner's existing source data, project solutions or completed assessments.
