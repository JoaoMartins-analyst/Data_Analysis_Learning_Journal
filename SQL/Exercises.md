# SQL — Exercise Records

Compiled on 11 October 2026 from [Notes.md](Notes.md) and the current roadmap. The supplied `SQL/Exercises.md` was empty.

## Evidence status

SQLBolt Lessons 1–18 and weekly foundation reviews are recorded as completed in the existing journal/roadmap. This review preserves that progress. However, the archive has no saved `.sql` submissions, database fixtures or query-result screenshots, so the original executable answers cannot be independently reviewed or faithfully reconstructed here.

The entries below are **retrospective summaries of reported practice**. They are not invented transcripts, new exercises, newly observed passes or a replacement for the independent Foundation assessment.

## Historical exercise index

| Session | Recorded exercise focus | Recorded lesson or correction |
|---|---|---|
| Day 1 | SELECT, WHERE, comparison operators, BETWEEN, IN, AND/OR | Several exercises reported completed; exact questions and queries absent |
| Day 2 | Equality and LIKE patterns | Clarify that equality and LIKE use collation rules; `%` and `_` are pattern wildcards |
| Day 3 | Filtering, ordering and LIMIT | Start with the business question; distinguish written clause order from logical evaluation |
| Day 4 | SQLBolt Lesson 4 review | “First” was misinterpreted; establish the requested sort order before selecting rows |
| Day 5 | SQLBolt Lessons 5 and 6: review, OFFSET and JOIN | Missing/incorrect ON logic caused repeated movie combinations; the notes report that the cause was understood |
| Day 6 / weekly review | Filtering, pagination and joins | LIMIT/OFFSET misunderstanding identified; distinguish actual logic from imprecise English wording |
| Day 7 | Outer joins and preserved rows | Select the required population; FULL OUTER JOIN is a concept, not native MySQL syntax |
| Day 8 | NULL and join aliases | Use IS NULL / IS NOT NULL; choose a non-nullable matched-side key for an unmatched-row test |
| Day 9 | Calculated result columns, AS and modulo | Calculating a result does not update stored data; even-year filtering was discussed |
| Day 10 / Week 2 review | Joins, NULL, expressions and aliases | NULL can occur in a source field; not every NULL means a join failed; avoid unnecessary joins |
| Day 11 | Aggregates and GROUP BY | Average employee tenure by role and total employee-years by building were practised; separate grain from measure |
| Day 12 | WHERE versus HAVING | Filter source rows versus aggregate groups; use the requested measure |
| Week 3 review | Grain, aggregates, joins and zero-order customers | Preserve the requested population; count the non-nullable order key after a LEFT JOIN |
| Day 14 | SQLBolt Lesson 12 and combined queries | Domestic plus international sales were initially interpreted as two separate totals; notes report a corrected interpretation |
| Week 4 review | Joins, aliases, grouping, order and requirements | COUNT(*) was repaired to COUNT(right-side key) for zero-match entities; full executable syntax remained a target |
| Day 17 | INSERT INTO | Name columns explicitly; auto-generated IDs depend on the actual schema |
| Day 18 | UPDATE, DELETE and apostrophes in strings | Preview affected rows; clear a field with NULL only if permitted; double embedded apostrophes |
| Day 19 | Integrated retrieval and CREATE TABLE | PRIMARY KEY does not automatically generate IDs; IF NOT EXISTS is not a schema migration |
| Day 20 | Integrated retrieval, multi-column sorting and ALTER TABLE | Sort direction applies per expression; DEFAULT is a fallback value, not proof of truth |
| Day 21 | SQLBolt through Lesson 18, DROP versus DELETE | Course completion reported; destructive schema changes need more than a SELECT preview |

The original notes do not contain a separate Day 15 SQL entry or exact calendar dates for these sessions. No entries or dates have been invented to fill those gaps.

## Reasoning recoverable from the notes

These are summarized explanations, not transcriptions of the original full queries.

### Requirement: return the first set of rows

- **Recorded difficulty:** interpreting “first” without using the required order.
- **Corrected reasoning:** decide the ordering, then apply OFFSET and LIMIT. Include a unique tie-breaker when a repeatable selection matters.
- **Missing evidence:** the original prompt, dataset, query, expected rows and actual output.

### Requirement: combine related tables

- **Recorded difficulty:** repeated movie combinations after a missing or incorrect join condition.
- **Corrected reasoning:** ON defines the relationship. Verify the keys and expected cardinality rather than removing duplicates to conceal a faulty join.
- **Missing evidence:** the original query and before/after result set.

### Requirement: retain customers with zero orders

- **Recorded correction:** use the customer population with a LEFT JOIN and count a non-nullable order key; COUNT(*) also counts the preserved unmatched row.
- **Important boundary:** a filter on the order table in WHERE can remove the zero-order customers again. Place conditions according to the actual question.
- **Missing evidence:** the original database fixture and executable submitted query.

### Requirement: calculate combined sales

- **Recorded difficulty:** interpreting domestic + international sales as two unrelated totals.
- **Corrected reasoning:** define the requested measure first, then produce that combined measure at the requested grain. Specify a missing-value policy instead of assuming NULL means zero.
- **Missing evidence:** the exact source columns, full question and verified output.

### Requirement: modify or remove data safely

- **Recorded practice:** INSERT, UPDATE, DELETE, CREATE, ALTER and DROP.
- **Current clarification:** a SELECT with the same WHERE condition can preview UPDATE/DELETE targets. It does not make a DROP or ALTER reversible. Practise schema changes on a disposable database and account for MySQL implicit commits.
- **Missing evidence:** the submitted statements and actual before/after data.

## What to save next

Keep working on Trail & Tide under its existing brief. Its complete MySQL queries, business questions and reconciliations will provide stronger evidence than rewriting every old SQLBolt exercise.

Save executable files in [queries](queries/README.md) for short practice, or in the relevant [project](../Projects/README.md) for integrated work. Link each file here and include the actual result or a small redacted result sample.

Do not put an AI-generated replacement query in the “my original answer” field. If a historical exercise is repeated now, label it as a new attempt with its real date and assistance used.

## Entry template — copy for each actual exercise

### [ID / date] — [Question title]

**Status:** Not attempted / attempted / reviewed / needs repair.

**Work type:** Guided practice / independent assessment.

**Database and version:** [Record the actual MySQL version when known.]

**Full question:** [Include filters, ties, sorting and whether zero-match entities must remain.]

**Tables and source:** [Names, relevant columns, keys and fixture path.]

**Expected grain:** [What one result row represents.]

**Expected result:** [Small hand-checked rows/counts/totals established before accepting AI output.]

**My initial query:** [Paste the actual query or link to the `.sql` file.]

**AI/tutor assistance:** [Exactly what help was used, or none.]

**Actual output:** [Record what was observed; leave pending until run.]

**Checks:** [Population, duplicate keys, NULL cases, joins, totals and one relevant boundary case.]

**Correction and rerun:** [If performed, include the changed query and observed result.]

**My explanation:** [Why this query answers the question and what it cannot establish.]

**Saved / committed / pushed:** [Record separately.]

**Assessment status:** [Guided success does not imply an independent pass.]
