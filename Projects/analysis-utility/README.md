# Phase 2 — Deterministic analysis utility

**Status:** Not started. **Task:** E2-07, with pandas and testing prerequisites.

Build a small Python/pandas utility that reads CSV data, validates keys/types, answers a defined business question and reconciles its result with SQL. Include an unfamiliar non-restaurant dataset somewhere in the Phase 2 work to demonstrate transfer.

## Acceptance evidence

- Clear input schema, grain, metric and units.
- Independent reference totals or hand-checked examples.
- Valid, empty, duplicate and malformed-input handling as relevant.
- Reconciled Python and SQL results.
- Tests that expose meaningful failures.
- A recorded dependency set and clean reproduction instructions.
- A concise explanation of the result and limits.

This utility becomes PA1's trusted calculation layer. Keep one implementation; the agent calls it instead of recreating its arithmetic with free-form text.

Use the [QA log](../../Templates/qa-log.md). Store actual implementation, fixtures and tests here when this stage starts.
