# Excel — Exercise Records

Compiled on 11 October 2026 from the submitted journal and eight workbooks.

## How to read this record

- **Workbook evidence:** the saved question/instructions, formulas and results can be inspected in the linked file. Formula examples below are transcribed from that evidence, with Excel’s internal compatibility prefixes removed for readability.
- **Reviewed calculation:** the reviewer independently recomputed the stated result from the saved inputs. This is not a new execution in Microsoft Excel and does not establish who wrote the formula or how much help was used.
- **Reported practice:** mentioned in [Notes.md](Notes.md), but its exact original question, submission or output is absent from this archive.
- **Review addition:** a clarification or proposed repair written during this review, not my historical answer or a completed new exercise.

Historical exercise dates and AI assistance were not recorded in the workbook files, so they are not invented here. Course answer tabs are references, not additional submissions. No independent assessment is marked passed by this document.

## EX-01 — Course gradebook

**Evidence:** [ExcelBasics01 Homework](workbooks/2.%20ExcelBasics01%20Homework.xlsx), `HW(1)`. The supplied reference is `HW(1an)`.

**Task, paraphrased:** build the pictured gradebook, calculate total points plus extra credit, percentage grades, decimal grades from the threshold table, and averages.

**Saved formulas and checks:**

| Location | Saved formula | Reviewed result |
|---|---|---|
| `M3` | `=SUM(C3:L3)` | Maximum score 750 |
| `M6`, spilling to `M13` | `=BYROW(C6:L13,SUM)+N3` | Totals: 664, 461, 496, 652, 698, 715, 370, 716 |
| `N6`, copied down | `=M6/$M$3` | First percentage 88.5333%; all eight agree with total / 750 |
| `O6`, spilling down | `=XLOOKUP(N6:N13,Q6:Q42,R6:R42,,-1)` | Grades: 3.4, 1.5, 1.9, 3.2, 3.7, 3.8, 0.7, 3.8 |
| `C14`, spilling across | `=BYCOL(C6:O13,AVERAGE)` | Average total 596.5; average decimal grade 2.75 |

**Review:** the checked calculations agree with the saved inputs. Here approximate lookup is intentional: select the exact threshold or next lower threshold. That rule is different from matching a product or student ID. The learner lookup includes rows through 42; the reference tab’s main lookup stops at row 40, so do not copy its shortened range for higher future grades.

## EX-02 — Recreated gradebook with synthetic data

**Evidence:** [ExcelBasics01 Recreation](workbooks/ExcelBasics01%20Recreation.xlsx), `Sheet1`.

**Recorded task:** recreate the previous table with different values and premises. Cell `A1` explicitly says the values are made up.

| Location | Saved formula | Reviewed result |
|---|---|---|
| `N3` | `=SUM(C3:M3)` | Maximum score 550 |
| `N6` | `=BYROW(C6:M13,SUM)+P3` | Totals: 524, 492, 470, 517, 478, 474, 475, 511 |
| `O6`, copied down | `=N6/$N$3` | Percentages agree with total / 550 |
| `P6` | `=XLOOKUP(O6:O13,R6:R14,S6:S14,,-1)` | Grades: 4, 3.8, 3.4, 4, 3.5, 3.5, 3.5, 4 |
| `C14` | `=BYCOL(C6:P13,AVERAGE)` | Average total 492.625; average grade 3.7125 |

**Saved reflections:** selection shortcuts, formatting, `F2`, reference anchoring with `F4`, `BYROW`, `BYCOL`, and lookup practice are recorded in `B17:B27`.

**Review correction:** the range used by `XLOOKUP` is a lookup table, not a PivotTable. These `BYROW` / `BYCOL` formulas spill multiple results; they are not single-output formulas in this example. The numeric calculations check out under the thresholds entered. Document that these are invented grading rules, not an official scale.

## EX-03 — Counts, criteria, OR logic and station summaries

**Evidence:** [ExcelBasics02 Homework](workbooks/2.%20ExcelBasics02%20Homework.xlsx).

### HW(1) — Basic and conditional totals

**Task:** count numeric sales cells, count populated sales-representative cells, total sales, and then count/sum for the specified representative and date.

| Cell | Saved formula | Reviewed result |
|---|---|---|
| `F5` | `=COUNT(C4:C12)` | 9 |
| `G5` | `=COUNTA(B4:B12)` | 9 |
| `H5` | `=SUM(C4:C12)` | 5,900 |
| `G11` | `=COUNTIFS(B4:B12,F11)` | 4 rows for Han |
| `H11` | `=SUMIFS(C4:C12,B4:B12,F11)` | 2,800 |
| `G13` | `=COUNTIFS(A4:A12,F13)` | 4 rows on the selected date |
| `H13` | `=SUMIFS(C4:C12,A4:A12,F13)` | 2,600 |

`COUNTA` works for the populated name cells here; it does not generally count words within text.

### HW(2) — Multiple criteria and a yearly report

**Task:** count Quad sales with a sales amount at least 2,200, sum their COGS, and calculate 2018 sales for each product.

```excel
H12: =COUNTIFS(D2:D665,H9,C2:C665,G9)
H13: =SUMIFS(E2:E665,D2:D665,H9,C2:C665,G9)
G24: =UNIQUE(SORT(C2:C665))
H24: =SUMIFS(D2:D665,B2:B665,G21,C2:C665,G24#)
```

`G9` contains Quad; `H9` contains `>=2200`; `G21` contains 2018.

**Reviewed results:** 16 qualifying sales and COGS of 18,618.82. The yearly product totals are:

| Product | 2018 sales |
|---|---:|
| Carlota | 64,136.97 |
| Quad | 76,460.24 |
| Sunset | 63,183.93 |
| Yanaki | 81,524.96 |

### HW(3) — OR within one field and across fields

**Task A:** sum and count sales for Carlota OR Quad.

```excel
H11: =SUM(SUMIFS(D2:D665,C2:C665,G8:G9))
H12: =SUM(COUNTIFS(C2:C665,G8:G9))
```

**Reviewed result:** sales 426,541.83 across 340 rows. These two distinct product values cannot both describe the same row, so adding their results is safe.

**Task B:** count sales and sum COGS where the year is 2017 OR the product is Quad.

```excel
H22: =SUM(IF((B2:B665=G20)+(C2:C665=H20),1,0))
H23: =SUM(IF((B2:B665=G20)+(C2:C665=H20),E2:E665,0))
```

**Reviewed result:** 353 rows and COGS of 225,592.51. There are 56 overlapping rows. `IF` selects each qualifying row once even when the added test equals 2. Summing the two raw counts would give 409 instead of 353.

**Presentation repair:** change `G12` and `G22` from “Total Sales” to “Number of sales” so counts are not confused with currency. The supplied answer sheet has its own count/value label mismatch at `G11:H12`; compare meaning and inputs, not just cell positions.

### HW(4) — Manufacturing-station performance

**Task:** for each station, count assembly times below three minutes and find the minimum time.

```excel
F9: =SEQUENCE(6)
G9: =COUNTIFS(B4:B471,F9#,C4:C471,G4)
I9: =SEQUENCE(6)
J9: =MINIFS(C4:C471,B4:B471,I9#)
```

| Station | Count below 3 min | Minimum time, min |
|---:|---:|---:|
| 1 | 0 | 4.0 |
| 2 | 46 | 1.7 |
| 3 | 51 | 1.5 |
| 4 | 44 | 1.6 |
| 5 | 5 | 2.3 |
| 6 | 10 | 2.5 |

**Review:** these results agree with all saved source rows. To make the existing “No Stations” parameter work, use `=SEQUENCE($G$5)` in both `F9` and `I9`. This still assumes station IDs are consecutive integers starting at 1; use the observed unique IDs if that assumption changes.

## EX-04 — Rounding and displayed precision

**Evidence:** [ExcelBasics03 Homework](workbooks/2.%20ExcelBasics03%20Homework.xlsx).

### HW(1) — Deduction per employee, then total

**Task:** calculate each employee’s tax deduction and sum those deductions.

```excel
C4: =ROUND(B4:B16*E4,2)
C17: =SUM(C4#)
```

**Reviewed results:** the first deduction is 77.62; all 13 rounded deductions total 952.37 at the supplied 1.475% rate.

### HW(2) — Explain the misleading display

**Original task:** explain what is misleading about the spreadsheet.

**Saved formula:** `C4 = B4*$E$4`, copied through `C16`. A sales value of 300 multiplied by 10.475% produces approximately 31.425 before rounding.

**Historical answer status:** there is no separate written answer in this workbook. The notes record that number formatting changes the display, whereas `ROUND` changes the number subsequently used.

**Review explanation:** displayed two-decimal values do not mean the underlying calculations have been rounded to cents. The mathematical total of unrounded deductions is 450.425; rounding each deduction to cents first gives 450.46. Decide which rule is required before changing a formula. This worksheet intentionally illustrates the distinction, so an unrounded formula here is not automatically a failed submission.

## EX-05 — Dates, months and working hours

**Evidence:** [ExcelBasics04 Homework](workbooks/2.%20ExcelBasics04%20Homework.xlsx).

| Sheet / question | Saved formula anchors | Reviewed result |
|---|---|---|
| `HW(1)` — days to pay invoices | `G5 = F5:F14-E5:E14` | 82, 8, 205, 164, 173, 102, 13, 246, 52, 178 days |
| `HW(2)` — project duration including both endpoint dates | `E5 = D5:D14-C5:C14+1` | 70, 220, 250, 198, 43, 55, 36, 233, 172, 238 days |
| `HW(3)` — due date two months later | `D5 = EDATE(C5,F6)` | Saved serial 46240 becomes 46301 |
| `HW(3)` — end of the same month | `D11 = EOMONTH(C11,F12)` | Saved serial 46240 becomes 46265 |
| `HW(4)` — same-day hours | `F8 = (E8:E17-D8:D17)*24` | First shift 7.5 hours; all ten checked |
| `HW(5)` — time-only overnight hours | `F8 = MOD(E8:E17-D8:D17,1)*24` | Overnight rows 14–17: 8, 8.25, 7.5, 9.5 hours |

Both pay sheets then use:

```excel
G8: =ROUND(F8#*C8:C17,2)
H8: =ROUND(G8#*H5,2)
I8: =G8#-H8#
```

**Reviewed results:** the first shift produces gross pay 187.05, deduction 14.31 and net pay 172.74. All ten pay rows in each of the two sheets agree with their inputs and row-rounding rule.

**Important boundary:** `MOD(...,1)` is suitable here because the input consists of times and the intended shift is below 24 hours. A 26-hour full-date-time interval must not become two hours. `+1` is appropriate for inclusive calendar dates, not automatically for every elapsed-time question.

## EX-06 — Conditional decisions and data-type checks

**Evidence:** [ExcelBasics05 Homework](workbooks/2.%20ExcelBasics05%20Homework.xlsx).

### HW(1-3) — Bonus and mobile-data rules

**Tasks:** decide whether sales reach the bonus threshold, return the bonus amount or zero, and decide whether data usage incurs an extra charge.

```excel
E5: =IF(D5>=$J$6,"Yes","No")
F5: =IF(D5>=$J$6,$J$7,0)
G5: =IF(C5<$J$12,"Under","Extra Charge")
```

These are copied down. The saved thresholds are sales of 10,000 for a bonus of 750, and data usage of 2.5 GB for an extra charge.

**Review:** all 20 rows match the stated rules. Equality belongs on the bonus-eligible and extra-charge sides. The existing data does not include every exact-boundary case; a future test at exactly 10,000 and 2.5 GB would establish that behaviour explicitly.

### HW(4) — Running bank balance

**Task:** update the previous balance if the date cell contains a number; otherwise show empty text.

```excel
G8: =IF(ISNUMBER(B8),G7-F8+E8,"")
```

**Reviewed sequence:** opening balance 5,000; then 4,500, 5,450, 5,394.75 and 5,545.20. Remaining date rows are empty and the saved formulas return empty text.

**Additional saved experiment:**

```excel
P8: =IF(ISNUMBER(B8:B18),OFFSET(F8:F18,-1,1)-F8:F18+E8:E18,"")
```

**Review clarification:** this matches the current balances, but `OFFSET` points to `G7:G17`. It depends on the original G-column calculation; it is not an independent spilled running balance. Retain the simpler copied formula as the clear solution. A gap inside the transaction list or a numeric non-date value needs a separate validation rule; `ISNUMBER` alone is not a complete date validator.

### HW(5) — Inclusive versus exclusive target

**Tasks:** calculate enrollment percentage, compare it with 70% using both `>=` and `>`, and translate each test into text.

```excel
G16: =F16/E16
H16: =G16:G31>=$F$13
I16: =G16:G31>$F$13
J16: =IF(G16:G31>=F13,"Target Met","No")
K16: =IF(G16:G31>F13,"Target Met","No")
```

**Review:** all 16 rows agree. The first two rows are exactly 70%: they meet `>=70%` and do not meet `>70%`. These are useful boundary cases already present in the workbook.

### HW(6) — Detect dates and amounts stored as text

**Task:** use logical formulas to identify text dates and text sales amounts; conversion is optional. The worksheet explicitly says the monthly report does not need to be changed for this exercise.

```excel
D13: =ISTEXT(B13:B32)
E13: =ISTEXT(C13:C32)
```

**Review:** the saved input cells in both ranges are numeric and the flags are all FALSE, which is consistent with the current file. The file does not preserve the before-conversion state, so the earlier text values cannot be reconstructed from this version.

**Separate report issue discovered during review:** `J14` is February 28, 2024. The monthly report excludes the February 29 entry at `B28:C28`, worth 1,180.11. February’s full total is 12,780.82, not 11,600.71. This boundary is also present in the supplied answer tab and does not invalidate the submitted type-checking formulas. See [the cell-level repair](Workbook-Review.md).

### HW(7) — All credit conditions must hold

**Task:** return Credit when assets exceed 2,500,000 AND rating is at least 5 AND late payments are below 6. Implement a spilled formula and a copied `AND` formula.

```excel
F12: =IF((C12:C21>D7)*(D12:D21>=D8)*(E12:E21<D9),"Credit","")
G12: =IF(AND(C12>$D$7,D12>=$D$8,E12<$D$9),"Credit","")
```

**Reviewed result:** three of the ten rows qualify. Both approaches agree with the source values.

### HW(8) — Any credit condition may hold

**Task:** repeat the decision using OR instead of AND, again with both implementations.

```excel
F12: =IF(OR(C12>$D$7,D12>=$D$8,E12<$D$9),"Credit","")
G12: =IF((C12:C21>D7)+(D12:D21>=D8)+(E12:E21<D9),"Credit","")
```

**Reviewed result:** seven of the ten rows qualify. The added condition is used as the `IF` test, so an overlapping match does not create extra output rows.

## EX-07 — Restaurant mini dataset

**Evidence:** [My mini Dataset 1](workbooks/My%20mini%20Dataset%201.xlsx), `Sheet1`.

**Task reconstructed from the saved worksheet:** calculate revenue per menu item and summarize quantity, price and revenue. The four historical questions at `A23:A26` are numbered but their actual wording is missing; the saved answers are 8,256.50, 750.59, 1,690 and 63. Their wording is not invented here.

```excel
E5: =C5:C15*D5:D15
C16: =BYCOL(C5:E15,SUM)
C17: =BYCOL(C5:E15,AVERAGE)
C18: =BYCOL(C5:E15,MAX)
C19: =BYCOL(C5:E15,MIN)
```

**Reviewed findings:**

| Measure | Value | Meaning |
|---|---:|---|
| Total quantity | 808 | Units sold across the 11 menu items |
| Revenue | €8,256.50 | Sum of quantity × price |
| Mean revenue per menu item | €750.59 | Total revenue / 11 menu items |
| Highest item revenue | €1,690 | Burrito |
| Lowest item revenue | €63 | Lime Mousse |
| Highest quantity | 130 | Burrito |
| Lowest quantity | 9 | Lime Mousse |

**Review additions, not historical answers:**

- The sum of listed prices at `D16` is 120; it is mathematically correct but should not be presented as a meaningful business total.
- `D17` is the unweighted mean listed price, approximately €10.91.
- A useful separate KPI is `=E16/C16`, average revenue per unit sold, approximately €10.22. This is not average customer spend.
- Revenue is not profit or contribution. There are no ingredient costs, VAT treatment, order counts or sales periods in this small table to support those conclusions.
- Record the source and whether the dataset is synthetic; the workbook does not explicitly settle that point.

## EX-08 — College grade consolidation and ranking

**Evidence:** [College Class Grading Rank](workbooks/College%20Class%20Grading%20Rank.xlsx), especially `AVGs` and `Ranking`.

**Task inferred from the implementation:** use the student master list to align grades from six source sheets by student ID, count the recorded numeric grades, calculate an average and sort students by that average. The original assignment and official grading policy are not present.

**Saved approach:**

```excel
AVGs!A2: =StudentNames[Student id]
AVGs!C2: =LET(x,XLOOKUP(A2:A31,'Pauta 1'!A2:A33,'Pauta 1'!B2:B33,"",0),IF(x="","",x))
AVGs!I2: =COUNT(C2:H2)
AVGs!J2: =AVERAGE(C2:H2)
Ranking!A2: =SORTBY(CHOOSE({1,2,3,4},AVGs!A2#,AVGs!B2#,AVGs!J2:J31,AVGs!I2:I31),AVGs!J2:J31,-1)
```

The other grade columns use corresponding exact-ID lookups into their source sheets. Count and average are copied down.

**Reviewed results:** all 30 master-list rows agree with the saved grade sources, counts and unweighted averages; the ranking is descending and carries the corresponding counts. No student names or IDs are reproduced in this journal entry.

**Policy questions to resolve before presenting this as a final ranking:**

- Three distinct IDs occur in grade source sheets but not in the 30-row master list. State whether that exclusion is intentional.
- Recorded grade counts are: 25 students with five grades, two with four, one with three, and two with one. Explain eligibility and whether the Pauta sheets represent alternatives or separately required assessments.
- State whether grades are equally weighted and how missing work, legitimate zero grades and ties should be handled. The current average of available numeric grades is not evidence of the official final-grade policy.
- The six `Exam` tabs are empty. Keep them only if they are intended future inputs; they are not completed evidence.
- Names, IDs and grades are present in the workbook. Confirm they are synthetic or create an anonymized demonstration copy before putting the file in a public portfolio.

## Reported daily practice not fully recoverable from these workbooks

This table preserves progress without pretending the original questions or submissions are available.

| Journal entry | Recorded activity | Evidence limit |
|---|---|---|
| Days 1–3 | Gradebooks, reference anchoring, counts and conditional sums | Workbooks above provide concrete examples; exact day-to-file timestamps are not established |
| Days 4–6 | Boolean arrays, retrieval and weekly review | Main OR reasoning can be checked in EX-03; all live tutor questions/answers are not saved |
| Day 7 | Formatting versus rounding | EX-04 supports this topic |
| Day 8 | Dates, month functions and working hours | EX-05 supports this topic |
| Days 9–10 | Conditional formulas, data types, missing values and Week 2 review | EX-06 supports much of this; exact Boss Battle submissions are absent |
| Days 11–12 / Week 3 | Lookups, FILTER, SWITCH, formula review and integrated assessment practice | Notes only for the full set; lesson-specific workbooks and exact responses are absent |
| Days 14–15 | PivotTables/charts/slicers, GROUPBY/PIVOTBY and Lesson 9 homework | Notes report completion; workbooks for Lessons 6–9 are not in this archive |
| Week 4 / Days 17–21 | Retrieval on grain, aggregation, lookups, types, dates and syntax | Reflections are present; original prompts and executable attempts are absent |

Do not repeat an entire completed course simply to populate this file. If the original exercise messages or missing workbooks are found, append their actual evidence. Otherwise use the next P1 work and assessment to demonstrate the skills now.

## Future exercise entry — copy when needed

### [ID / date] — [Question title]

- **Full question and constraints:**
- **Dataset / workbook / sheet / cells:**
- **My first formula or answer:**
- **Expected result and independent check:**
- **Actual output:**
- **AI or tutor help used:**
- **Correction and observed rerun:**
- **Business interpretation and limitation:**
- **Status:** attempted / reviewed / needs repair; record an assessment pass separately.
- **Saved / committed / pushed:** record separately.
