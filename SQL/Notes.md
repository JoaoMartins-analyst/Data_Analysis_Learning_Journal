##  Day 1



- I learned how to use the select and where functions, along with operators like BETWEEN/NOT BETWEEN, AND/OR, IN/NOT IN and =,!=,<,<=,>,>=

- Practiced and completed a few exercises using this knowledge.



## Day 2



- = means EXACT match

- LIKE means PATTERN match

- % means "anything can go here"



## Day 3



I learned:



- WHERE filters data based on conditions.

- ORDER BY sorts the returned results.

- LIMIT restricts the number of rows returned.

- Typical query flow:

&#x20; SELECT → FROM → WHERE → ORDER BY → LIMIT

- Before writing SQL, define the business question you are trying to answer.

- The same SQL concept can be explained differently depending on the audience (business vs. technical).



## Day 4



- Reviewed SQLBolt Lesson 4 after realizing my mistake wasn't SQL syntax but requirement interpretation.



### Key takeaways

- Read requirements carefully before writing the query.

- "First" usually refers to the rows after applying `ORDER BY`, not the earliest records.

- Always ask: "First according to what?"



\### Reflection

A wrong answer doesn't always mean I misunderstood SQL. Sometimes I simply interpreted the business requirement differently. Finding the exact misunderstanding is part of becoming a better analyst.

## Day 5

Completed SQLBolt Lessons 5 and 6.

### Key takeaways
- `IN` checks whether a value belongs to a list of possible values.
- `OFFSET` specifies how many sorted rows SQL should skip.
- `JOIN` combines information from related tables.
- The `ON` clause defines which rows from each table should match.
- Without the correct join condition, SQL can produce many repeated combinations of rows.

### Reflection
Lesson 6 was straightforward once I understood that `ON` is what defines the relationship between the two tables. Forgetting it caused repeated movie names, but diagnosing the mistake helped clarify how joins work.

## Day 6 — Weekly Review

Reviewed filtering, sorting, pagination, and joins through a boss battle.

### Key takeaways
- `LIMIT` and `OFFSET` work together to select a section of an ordered result.
  - `OFFSET` decides where the section begins.
  - `LIMIT` decides how many rows are returned.
- The base table should be chosen by the result's grain: what one returned row represents.
- `JOIN` combines related data from different tables.
- `ON` matches rows by comparing related key values.
- `JOIN` normally means the same as `INNER JOIN`.
- Use single quotes for text values, such as `'Portugal'`.
- Qualifying column names with their table names makes joined queries clearer.

### Reflection
The review exposed a real misunderstanding about `LIMIT` and `OFFSET`. I also learned to distinguish between a logical mistake and English wording that does not accurately express my intended reasoning.

## Day 7

- Learned that `LEFT OUTER JOIN` and `RIGHT OUTER JOIN` keep all rows from one selected table, while `FULL OUTER JOIN` keeps all matching and unmatched rows from both tables.
- When an outer join preserves a row without a match, the missing side’s columns contain `NULL`.
- Practiced choosing the simplest query based on the requirement instead of forcing the newest SQL concept into every solution.

## Day 8

- Learned that `NULL` represents missing or unknown information rather than an ordinary value.
- Used `IS NULL` and `IS NOT NULL` because ordinary comparisons such as `= NULL` do not work.
- Practiced using `NULL` to identify matched and unmatched rows after an outer join.
- Learned that joined queries can qualify columns with full table names or shorter table aliases for clarity.

## Day 9

- Learned how SQL expressions can perform calculations on stored values without changing the underlying table.
- Used `AS` to give calculated result columns meaningful names.
- Practiced converting values using arithmetic expressions, such as converting a 0–10 rating into a percentage.
- Learned that `%` is the modulo operator and returns the remainder after division.
- `WHERE year % 2 = 0` keeps years whose division by 2 has a remainder of 0.
- Reinforced the principle of choosing the simplest query that answers the business requirement instead of forcing newly learned syntax into every solution.

## Day 10 — Week 2 Boss Battle

- Reviewed `INNER JOIN`, `LEFT OUTER JOIN`, `NULL`, expressions, aliases, sorting, and modulo.
- Reinforced that `NULL` means a specific field has a missing or unknown value; it is not limited to failed joins.
- Practiced using `LEFT OUTER JOIN` plus `IS NULL` to find records with no match in another table.
- Reinforced choosing the correct column for `IS NULL` based on the business question rather than simply testing any nullable field.
- Practiced calculated columns using expressions and `AS` without changing the stored table data.
- Reinforced using single quotes for SQL strings, such as `'Portugal'`.
- Practiced avoiding unnecessary joins when the required information already exists in one table.

## Day 11 — Aggregate Queries and GROUP BY

- Learned the aggregate functions `MAX`, `MIN`, `AVG`, `SUM`, and `COUNT`.
- An aggregate without `GROUP BY` summarizes the qualifying dataset into one overall result.
- `GROUP BY` divides rows into groups and calculates the aggregate separately for each group.
- Practiced calculating average employee tenure by role and total employee-years by building.
- Reinforced the difference between result grain and the measure being calculated.
  - Example: one row = one department is the grain.
  - Highest salary in that department is the measure.
- Reinforced that the aggregate function must match the business question: `SUM` and `COUNT` may both return valid numbers but represent different things.

## Day 12 — Aggregate Queries and HAVING

- Reinforced aggregate functions such as `AVG`, `SUM`, `COUNT`, `MIN`, and `MAX`.
- Reviewed that `GROUP BY` changes the result grain by creating one aggregate result per group.
- Learned the distinction between `WHERE` and `HAVING`.
  - `WHERE` filters individual source rows before grouping.
  - `HAVING` filters grouped or aggregated results after grouping.
- Practiced using `HAVING` for conditions based on aggregate values, such as `HAVING AVG(salary) > 3000`.
- Learned that some conditions on grouping columns can technically be expressed using either `WHERE` or `HAVING`, but `WHERE` is generally clearer when the condition can be evaluated on the original rows.
- Reinforced separating result grain from the measure being calculated.

## Week 3 — Boss Battle

- Reviewed exact-match lookup logic and reinforced using `XLOOKUP` for identifiers where approximate matching would be inappropriate.
- Reinforced the difference between a technical lookup failure and a business rule, including why missing product data should not automatically be converted to a zero price.
- Reviewed the Golden Rule, absolute references, data-type conversion, `FILTER`, Boolean logic, and transaction-level rounding.
- Identified requirement-reading as an important QA risk, particularly around words such as AND and OR.
- Reinforced `LEFT JOIN` and `IS NULL` for identifying unmatched records.
- Reviewed aggregates, result grain, `GROUP BY`, `WHERE`, and `HAVING`.
- Reinforced the distinction between source fields and aggregate measures.
- Practiced preserving the full requested population, including using `LEFT JOIN` and `COUNT(orders.order_id)` when customers with zero orders must remain in the result.
- Added a requirement pre-flight check for future projects and Boss Battles: grain, required output, measure, filters, Boolean logic, and aggregation stage.

## Day 14 — SQL

- Completed SQLBolt Lesson 12.
- Reinforced SQL's conceptual execution order: FROM/JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT/OFFSET.
- Learned why SELECT aliases are usually unavailable in WHERE/HAVING but can normally be used in ORDER BY.
- Practiced combining JOIN, WHERE, GROUP BY, SUM, AVG, COUNT, and HAVING.
- Reinforced that WHERE filters source rows while HAVING filters aggregated groups.
- Misread a requirement asking for combined domestic + international sales as two separate totals; corrected the interpretation.
- Continued practicing requirement parsing before writing the query.

## Week 4 Boss Battle — SQL

- Strong retrieval: `WHERE` vs `HAVING`, aggregation, `GROUP BY`, logical execution order, aliases, joins, grain, and requirement interpretation.
- Repaired `LEFT JOIN` counting: use `COUNT(right_table.key)` instead of `COUNT(*)` when unmatched entities must remain at 0.
- Base-table choice should follow the population the business requirement says must be preserved.
- Main weakness remains small implementation mistakes after correct reasoning, such as missing clauses, typos, or incomplete syntax.
- Main QA habit: state the logic first, then write the full executable query.

## Day 17 - SQL

- Learned `INSERT INTO` to add new rows to an existing table.
- Auto-generated ID columns do not need to be manually supplied when the database generates them.
- Explicitly naming columns in an `INSERT` makes the query clearer and less dependent on the table's current structure.
- `SELECT` reads existing data, while `INSERT` changes stored data, so mistakes with `INSERT` carry greater data-integrity risk.
- Continued practicing full executable SQL syntax instead of shorthand.

## Day 18 - SQL

- Learned `UPDATE` to modify existing values and `DELETE` to remove rows.
- `WHERE` determines which rows are affected; omitting it can modify or delete the entire table.
- Practiced verifying destructive conditions with `SELECT` before executing them.
- To remove one field value while keeping the row, use `UPDATE ... SET column = NULL`.
- Learned to escape apostrophes inside SQL strings by doubling them, for example `'O''Brien'`.
- Reinforced the higher data-integrity risk of SQL commands that modify stored data.

## Day 19 - SQL

- Used integrated retrieval combining joins, filters, aggregation, `GROUP BY`, `HAVING`, aliases, ordering, NULL behavior, and population-preserving joins.
- Reinforced using `LEFT JOIN` with `COUNT(right_table.key)` to preserve zero-match entities correctly.
- Practiced verifying destructive conditions with `SELECT` before `DELETE`.
- Learned `CREATE TABLE`, column data types, and constraints such as `PRIMARY KEY`, `NOT NULL`, and `UNIQUE`.
- `IF NOT EXISTS` prevents duplicate table creation but does not modify an existing table schema.
- Repaired the distinction between `PRIMARY KEY` and auto-generated IDs: a primary key does not automatically imply `AUTO_INCREMENT`.

## Day 20 - SQL

- Used integrated retrieval combining joins, population/grain, aggregation, `WHERE`, `GROUP BY`, `HAVING`, aliases, and multi-column ordering.
- Learned that sort direction such as `ASC` or `DESC` applies individually to each expression in `ORDER BY`.
- Reinforced when `COUNT(*)` is safe and why `COUNT(right_table.key)` is needed with zero-match `LEFT JOIN` populations.
- Learned `ALTER TABLE` to modify an existing table schema, including adding columns with `ADD COLUMN`.
- Learned `DEFAULT` as the value used when a column value is omitted, not proof that the value is factually correct.
- Reinforced the distinction between schema changes (`CREATE` / `ALTER`) and data changes (`INSERT` / `UPDATE` / `DELETE`).

## Day 21 - SQL

- Completed SQLBolt through Lesson 18.
- Used integrated retrieval across joins, aggregation, `WHERE`, `GROUP BY`, `HAVING`, `IN`, `ORDER BY`, `LIMIT`, and zero-match `LEFT JOIN` logic.
- Learned `DROP TABLE` to remove an entire table and distinguished it from `DELETE`, which removes rows while preserving the table.
- `IF EXISTS` prevents an error when the target table is already absent, but destructive commands should still be verified carefully before execution.
- Reinforced the workflow of inspecting targets with `SELECT` before `UPDATE`, `DELETE`, or other destructive operations.
- SQL concepts and command selection are stronger than exact syntax retrieval, especially for the newer `INSERT` / `UPDATE` / `DELETE` / `CREATE` / `ALTER` / `DROP` statements.

