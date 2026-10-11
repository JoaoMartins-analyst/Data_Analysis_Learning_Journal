# Workbook Review — 11 October 2026

## Result and scope

The saved calculations are generally consistent with their inputs. The most useful improvements concern date boundaries, metric definitions, documented business rules and clear evidence.

Reviewed eight workbooks containing 54 worksheets, including reference and empty sheets. The review inspected saved data, formulas, shared/dynamic-array definitions and cached results, and independently recomputed 803 learner-sheet result cells in a separate calculation script. Those checked values matched the submitted results within floating-point tolerance. That does **not** mean every report answers the intended business question: the February boundary issue below is a concrete example.

This was a file/formula review, not a live Microsoft Excel recalculation or a full visual/compatibility test. It cannot prove independent authorship, assess unsaved changes, or mark a roadmap assessment passed. Existing workbooks were not modified.

## 1. Correct the February reporting boundary

**File:** [ExcelBasics05 Homework](workbooks/2.%20ExcelBasics05%20Homework.xlsx).

**Sheet:** `HW(6)`; the same boundary appears in `HW(6an)`.

| Evidence | Saved value | Consequence |
|---|---|---|
| `I14` | 1 February 2024 | Correct beginning of month |
| `J14` | 28 February 2024 | Excludes the leap day |
| `B28:C28` | 29 February 2024; 1,180.11 | Omitted from the monthly result |
| `K14` | 11,600.71 | Correct for the specified interval, incomplete for the full month |
| Independently calculated full February | 12,780.82 | Includes the missing sale |

The exercise asks for text detection and explicitly says the monthly report does not need to be changed. Your `ISTEXT` formulas fit the saved data; the pre-existing report issue is a separate QA finding.

**Minimal proposed repair:** set `J14` to:

```excel
=EOMONTH(I14,0)
```

The current data contains whole dates, so the existing inclusive end-date `SUMIFS` would then include February 29. For all three month-end display cells, put `=EOMONTH(I13,0)` in `J13` and copy through `J15`.

**More robust reporting formula:** replace the array formula at `K13` with:

```excel
=SUMIFS(C13:C32,B13:B32,">="&I13:I15,B13:B32,"<"&EDATE(I13:I15,1))
```

This assumes `I13:I15` contains each month’s first day at midnight. It includes dates/times from that point up to, but not including, the next month’s first day. It handles leap years and transactions with time components without requiring a last-moment-of-month timestamp. Keep the display end dates consistent even though this formula does not depend on column J.

**Checks to perform after editing:** January 9,000.45; February 12,780.82; March 5,669.85; total 27,451.12, matching all 20 numeric sales rows. In a separate small test copy, check that February 29 at 23:59 is included and March 1 at 00:00 is excluded from February. These edits and boundary tests are proposed, not recorded as already performed in Excel.

[Microsoft’s EOMONTH reference](https://support.microsoft.com/en-us/excel/functions/eomonth-function) documents the month-end function. The omitted value and repaired totals above come from this submitted workbook.

## 2. Give restaurant summaries their actual business meaning

**File:** [My mini Dataset 1](workbooks/My%20mini%20Dataset%201.xlsx), `Sheet1`.

All 11 item-revenue calculations and the saved column summaries agree with the inputs. Improve interpretation as follows:

| Location / measure | Finding | Improvement |
|---|---|---|
| `E16` | Revenue €8,256.50 | Label it total revenue, not profit |
| `C16` | 808 units | Make the unit explicit |
| `D16` | Sum of menu prices = 120 | Remove or label “sum of listed prices — not a business KPI” |
| `D17` | Unweighted mean listed price ≈ €10.91 | State it gives each of the 11 menu items equal weight |
| `E17` | Mean item revenue ≈ €750.59 | Label “average revenue per menu item” |
| Suggested separate cell | `=E16/C16` ≈ €10.22 | Label “average revenue per unit sold” |
| `B23:B26` | Four numeric answers, without full questions | Add their original questions if recoverable; the review does not invent them |

Because `C16` is a spilling `BYCOL` formula across `C16:E16`, do not try to type over `D16` while it remains part of that spill. To remove the meaningless price total, replace the single `C16` anchor with `=SUM(C5:C15)`, leave `D16` empty, and put `=SUM(E5:E15)` in `E16`. The other summary rows can remain if labelled clearly.

The largest revenue is Burrito at €1,690; the smallest is Lime Mousse at €63. There is no sales period, cost data or customer/order count, so this table alone cannot establish profit, sales trends or average customer spend. Add provenance and the intended decision before treating it as a portfolio business case.

## 3. Clarify the grade-ranking policy and publication status

**File:** [College Class Grading Rank](workbooks/College%20Class%20Grading%20Rank.xlsx).

The 30 master-list rows have consistent saved grade lookups, counts and unweighted averages. The ranking is descending and keeps the corresponding count with each student. Showing the count is useful.

The questions to settle are about the analysis specification:

- Three distinct student IDs appear in source grade sheets but are not in the 30-row master list. If only the master list is the intended population, state that explicitly; otherwise resolve the exclusions.
- Twenty-five students have five recorded numeric grades, two have four, one has three and two have one. Decide whether these are comparable final results and whether some Pauta sheets are alternatives. Do not assume all six are compulsory.
- Document the weighting, missing/absent-work policy, legitimate zero grades, eligibility and tie handling. Until that is agreed, “mean of recorded grades” is a safer description than an official final grade.
- Check a synthetic zero-grade and a missing-grade example separately before generalizing the lookup/missing-value handling.
- The `Exam 1`–`Exam 6` sheets are empty. They are future placeholders, not completed work.
- Names, student IDs and grades are present. Confirm that they are synthetic or produce an anonymized demonstration copy before publishing this workbook. Removing names alone would still leave the IDs.

No identifiable student records are reproduced in this review, and the original workbook has not been changed.

## 4. Small implementation and documentation improvements

| Workbook / location | Finding | Suggested action |
|---|---|---|
| ExcelBasics02 `HW(4)!F9`, `I9` | Both use `SEQUENCE(6)` despite an existing “No Stations” input at `G5` | Use `=SEQUENCE($G$5)` when consecutive station IDs are the intended model |
| ExcelBasics02 `HW(3)!G12`, `G22` | “Total Sales” labels counts | Rename to “Number of sales” |
| ExcelBasics02 reference `HW(3an)!G11:H12` | Count and sales-value labels are mismatched | Treat reference tabs critically; your own sum/count calculations agree with the raw data |
| ExcelBasics01 Recreation `B24` | Calls the lookup range a PivotTable | Change the description to “lookup table” |
| ExcelBasics01 Recreation `B27` | Describes BYCOL/BYROW as single-output in this example | Describe them as spilling arrays here; aggregation and output shape are separate concepts |
| ExcelBasics05 `HW(4)!P8` | OFFSET points to the already-computed balances in `G7:G17` | Label this as a dependent alternative experiment; the copied G-column formula is the clear main solution |
| College grade workbook | Source/rule explanation is missing | Add a short project brief before using it as portfolio evidence |

The changes above are documented suggestions, not edits already applied to the workbooks.

## Workbook-by-workbook review summary

| Workbook | What was checked | Outcome / limit |
|---|---|---|
| ExcelBasics01 Homework | Maximum score; eight totals, percentages and threshold grades; column averages | Checked numeric results agree; learner lookup includes the full supplied threshold table |
| ExcelBasics01 Recreation | Maximum score; eight totals, percentages and threshold grades; column averages | Checked results agree with invented values/rules; correct two explanatory labels |
| ExcelBasics02 Homework | Conditional sums/counts over all 664 sales rows; yearly product report; OR overlap; station reports over 468 rows | Checked results agree; improve count labels and parameter reference |
| ExcelBasics03 Homework | Thirteen rounded deductions and total; thirteen unrounded illustrative deductions | Arithmetic agrees; keep the distinction between the intentional teaching example and a required rounding policy |
| ExcelBasics04 Homework | Date differences; inclusive durations; month functions; all same-day/overnight hours and pay rows | Checked results agree; document the time-only, sub-24-hour assumption for MOD |
| ExcelBasics05 Homework | Bonus/data decisions; running balances; enrollment boundaries; type flags; monthly intervals; AND/OR eligibility | Current formula outputs agree with inputs; full-month report has a leap-day omission |
| My mini Dataset 1 | Eleven item revenues and all column aggregates | Arithmetic agrees; improve grain, KPI labels and provenance |
| College Class Grading Rank | Thirty master rows against six grade sources; counts, averages and sorted outputs | Current calculations agree; official policy/population and publication status need clarification |

## What this archive does not establish

- The original wording of all live tutor questions or the amount of assistance used.
- Execution of past SQL questions: no `.sql` submissions were included.
- The full Lesson 6–9 Excel work, despite their recorded completion in the notes/roadmap.
- The finished Trail & Tide project or an independent Foundation assessment pass.
- Live Excel recalculation, changes under new inputs, complete formatting quality, or compatibility with a different Excel version.

These limits do not erase completed learning. Add evidence as it becomes available and use the next project/assessment to demonstrate the skills independently.
