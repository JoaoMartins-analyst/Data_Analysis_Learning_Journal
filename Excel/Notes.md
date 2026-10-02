## Day 1



- I learned to format tables, pivot tables and functions. I also learned XLOOKUP.

- I learned about the difference about aggregate, single output and spilled array formula.

- I built and formatted a functional table and pivot table with this knowledge.



## Day 2



What I remembered easily:

- Absolute references

- SUM

- Basic table layout

- XLOOKUP and how to retrieve information from outside tables

-. the use of F2 to edit a cell and F4 to make a cell's value absolute when using a function with an array of cells



What I had to think about:

- Percentage formula

- Column organization



## Day 3

What I learned:

- COUNT counts numeric cells only.

- COUNTA counts all non-empty cells.

- ROWS counts the number of rows, regardless of contents.

- Choose functions based on the business question, not on which one is "more powerful."

- Dynamic arrays spill automatically; use # to reference the entire spill range.

- SORT(UNIQUE(...)) is generally more efficient than UNIQUE(SORT(...)) because duplicates are removed before sorting.

- Think in terms of business problems first, formulas second.



## Day 4

Focused on understanding the logic behind array formulas instead of learning new functions.



### Key takeaways

- `IF` does not perform the logical test—it only decides what to return based on TRUE/FALSE.

- `+` works as OR, `\*` works as AND.

- Parentheses change the meaning of logical expressions (same principle as PEMDAS).

- Before choosing a formula, think about the business logic:

&#x20; - If conditions cannot overlap (e.g. 2024 OR 2025), separate `COUNTIFS` + addition is fine.

&#x20; - If conditions can overlap (e.g. 2024 OR Product = "Razer"), use logical array formulas to avoid double-counting.



### Reflection

Today's biggest improvement wasn't learning a new function—it was learning to translate business questions into logical expressions before writing formulas.

## Day 5

- - Repeated Day 3's homework as a retrieval exercise. I made a few logical mistakes, but identified and corrected them independently because I understood what each formula was instructing Excel to do.

## Day 6 — Weekly Review

Reviewed logical array formulas through retrieval and mixed business questions.

### Key takeaways
- Logical tests return TRUE/FALSE values.
- `+` represents OR and `*` represents AND.
- Parentheses determine which conditions belong together.
- `IF` converts any non-zero logical result into the chosen output.
- When OR conditions can overlap, separate counts may double-count the same row.
- Text criteria such as `"Portugal"` and `"Razer"` require quotation marks.

### Reflection
I retained the main concepts well. My biggest challenge was expressing the logic precisely in English, rather than understanding how the formulas worked.

## Day 7

- Reviewed Week 1 concepts to confirm that nested logical expressions, joins, and pagination had been consolidated.
- Learned that number formatting changes only how a value is displayed, while `ROUND` returns a new rounded value that later calculations can use.
- Understood why displayed values may appear not to equal a displayed total: Excel still calculates with the full stored precision.

## Day 8

- Learned how Excel stores dates as whole numbers and times as fractions of a day.
- Practiced calculating date durations, including using `+1` when both the start and end dates must be counted.
- Used `EDATE` to move a date by a number of months and `EOMONTH` to return the final day of a month.
- Calculated working hours by subtracting times and multiplying by 24, and used `MOD(...,1)` to handle shifts that cross midnight.


## Day 9

- Reviewed Day 8 material and reinforced the meaning of `NULL` before starting new content.
- Practiced `IF`, `AND`, `OR`, `ISNUMBER`, `ISTEXT`, comparison operators, and `IFNA`.
- Reinforced that logical tests return TRUE/FALSE, while `IF` determines what value should be returned for each result.
- Learned that `ISNUMBER` and `ISTEXT` only prove what a value is when they return TRUE; a FALSE result does not automatically identify the value's type.
- Learned that `IFNA` replaces only `#N/A` errors and otherwise returns the original result.
- Corrected a running-balance reference mistake: cumulative calculations must use the previous balance rather than repeatedly referencing the starting value.

## Day 10 — Week 2 Boss Battle

- Reviewed date and time logic, including inclusive date counting, `EDATE`, `EOMONTH`, and how Excel stores time as fractions of a day.
- Reinforced `IF`, `IFNA`, `ISNUMBER`, `ISTEXT`, and mixed AND/OR logic using `*`, `+`, and parentheses.
- Confirmed that `IFNA` should preserve the original result unless the formula returns `#N/A`.
- Reinforced the difference between a technical result and a business rule: `#N/A` means a lookup failed, while what to do with that result depends on the business requirement.
- Revisited result grain: one row should represent the entity the business question is asking about.

## Day 11 — Lookup, Filter and Selection Functions

- Reinforced `XLOOKUP` for flexible lookups that return a corresponding value.
- Learned that `LOOKUP` can be useful for simpler lookups when the lookup values are sorted in ascending order, such as tax brackets, commissions, or shipping-weight tables.
- Learned that `XMATCH` returns the relative position of a value within an array rather than returning a corresponding value.
- Learned to use `FILTER` to return all records that satisfy one or more logical conditions.
- Reviewed using `*` as AND logic inside `FILTER`.
- Learned that `SWITCH` can choose between different results or arrays based on a selected value.
- Practiced combining functions, such as using `SWITCH` to select a pricing table and `LOOKUP` to retrieve a value from it.
- Reinforced choosing functions based on the business requirement rather than using the most powerful function automatically.

## Day 12 — Comprehensive Formula Review

- Reviewed Excel's Golden Rule: values that may change should be stored in labeled cells and referenced in formulas rather than hard-coded.
- Reinforced the difference between relative, absolute, and mixed cell references.
- Reviewed operator precedence and the importance of parentheses when controlling calculation order.
- Reinforced the distinction between stored values and number formatting.
- Reviewed different formula types, including copied formulas, dynamic arrays, scalar array formulas, and Excel Table formulas.
- Learned that values which look numeric can still be stored as text and may need conversion using methods such as `--` or `VALUE()`.
- Reinforced that correct data types are important for predictable calculations and analysis.
- Practiced `ROUND`, `MROUND`, `CEILING.MATH`, and `FLOOR.MATH`.
- Learned that rounding individual values before summing can produce a different result from summing full-precision values and rounding only the final total.
- Reinforced choosing `XLOOKUP` for exact identifier matches and using `LOOKUP` appropriately for sorted threshold-style lookups.
- Practiced combining formula logic with business rules rather than choosing functions only by syntax.

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

## Day 14 — Excel

- Learned how to create and use PivotTables, PivotCharts, and slicers.
- Reinforced the difference between raw data and summarized information.
- Practiced identifying dimensions and measures in PivotTables.
- Learned that PivotTable grain can be defined by multiple dimensions, such as Month × SalesRep.
- Reinforced that the business question determines whether a numeric field should use COUNT, SUM, AVG, etc.
- Used Excel Tables as dynamic PivotTable sources; new rows are included after refreshing the PivotTable.
- Practiced formatting PivotChart axes and setting custom bounds.

## Day 15 — Excel

- Completed ExcelIsFun Lesson 9 and homework on `GROUPBY` and `PIVOTBY`.
- Learned that `GROUPBY` can use multiple row fields; multiple dimensions do not automatically require `PIVOTBY`.
- `PIVOTBY` is mainly useful when a dimension needs to be displayed across columns or when a PivotBy-specific feature is required.
- Practiced `PERCENTOF`, Data Validation dropdowns, text-number coercion with `+0` / `--`, and chart number/date formatting.
- Checked the homework answer workbook and found that its chart skips several summary rows and its source Units data differs from the homework dataset.

## Week 4 Boss Battle — Excel

- Strong retrieval: PivotTable grain/refresh, formatting vs stored values, date display formatting, and Boolean `AND` logic.
- Needed repair: `GROUPBY` vs `PIVOTBY`, full function syntax, and lookup vs aggregation.
- `GROUPBY` can use multiple row fields; `PIVOTBY` is used when a dimension needs to be displayed across columns.
- When multiple qualifying rows must be combined into one result, use aggregation such as `SUMIFS` or `GROUPBY`, not `XLOOKUP`.
- Main QA habit: write the full executable formula instead of shorthand during assessments.

## Day 17 - Excel

- Used spaced retrieval to reinforce `GROUPBY` vs `PIVOTBY`, lookup vs aggregation, percentage formatting, and PivotTable grain.
- `GROUPBY` is enough when dimensions remain in row fields; `PIVOTBY` is useful when a dimension is displayed across columns or a PIVOTBY-specific feature is needed.
- Reinforced using `SUMIFS` instead of `XLOOKUP` when multiple qualifying rows must be aggregated.

## Day 18 - Excel

- Used spaced retrieval to reinforce `GROUPBY`, grain, and conditional aggregation with `AVERAGEIFS`.
- Reinforced that normal `GROUPBY` output has row grain, while pivot-style cross-tabs use detailed value-cell grain.
- Continued choosing the simplest aggregation tool that directly answers the business requirement.

## Day 19 - Excel

- Used a longer integrated retrieval block to revisit older Month 1 material before the project.
- Reinforced lookup vs aggregation: `XLOOKUP` retrieves one matching record, while `SUMIFS` / `GROUPBY` combine multiple qualifying rows.
- Revisited overnight time calculations with `MOD` and Boolean logic using `+` for OR and `*` for AND.
- Reinforced row grain vs detailed value-cell grain and the use of `GROUPBY` for dynamic grouped summaries.
- Main repair areas: `MOD` syntax, XLOOKUP direction across table grains, and writing full executable formulas.

## Day 20 - Excel

- Used broad integrated retrieval across older Month 1 Excel material before the project.
- Reinforced many-to-one lookup direction: each transaction can safely retrieve attributes from a unique master record, while `XLOOKUP` should not collapse multiple matching transaction rows.
- Revisited inclusive date calculations, formatting vs `ROUND`, absolute references, structured references, and dynamic-array spilling.
- Reinforced `FILTER` + `SORT`, Boolean conditions, and spill-range references such as `G2#`.
- Main retrieval gaps: exact syntax for older formulas, current-row structured references, and distinguishing table propagation from dynamic-array spilling.
