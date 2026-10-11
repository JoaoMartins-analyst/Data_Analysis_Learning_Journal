# AI-assisted analysis and automation

**Entry focus:** practical agent/API competence for analysis work.

| Folder | Evidence |
|---|---|
| [prompts](prompts/README.md) | Bounded task specifications and versioned prompts |
| [api-labs](api-labs/README.md) | HTTP/JSON, local model API and validated tool-call experiments |
| [evaluations](evaluations/README.md) | Independent expectations and observed outcomes |
| [run-logs](run-logs/README.md) | Redacted run traces, failure/recovery and time comparisons |

Understand the model, instructions, tools, host execution, state/memory and stopping conditions. Use the model where flexible interpretation helps; use checked deterministic code for exact metrics.

The initial setup trial follows P1 and its Foundation assessment. The new conversation's sequence is a brief API introduction, then a small Windows/Ollama/Odysseus experiment capped at one or two study sessions. Record what actually worked. Installation is not proof of API competence, and Odysseus is not a prerequisite for continuing study.

Phase 2 uses direct Python API calls, schema checks, an allowlisted tool loop, scheduling, logs and recovery. The integrated implementation lives in [PA1](../Projects/pa1-unattended-analysis-assistant/README.md), reusing the [analysis utility](../Projects/analysis-utility/README.md).

Use the [AI work log](../Templates/ai-work-log.md) to document assistance. Use the [agent run template](../Templates/agent-run.md) for executed workflows. Label mocks, real local calls and hosted calls distinctly.

No paid API subscription, advanced agent framework, RAG system or TypeScript interface is added to this entry stage.

## Saving study work

Continue [Notes.md](Notes.md) and [Exercises.md](Exercises.md). Keep prompts, API labs, evaluations and run logs in their existing subfolders and link the evidence from each exercise.
