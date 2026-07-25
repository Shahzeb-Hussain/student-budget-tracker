# Student Budget Tracker (Excel)

## Problem Statement

This dashboard helps a student track exactly where their money is going each month, using a live bank statement export. It shows opening vs. closing balance at a glance, splits total money in vs. money out, and — using XLOOKUP pulled live from the Transactions sheet — breaks spending down by category against a personal budget limit for each one. This makes it immediately obvious which categories are on track, which are close to their limit, and which have blown past it, so spending habits can be corrected before the next statement rather than after.

It also tracks progress toward multiple savings goals (Laptop, Vacation, Emergency Fund, New Phone, Books/Study) side by side, so saving isn't an afterthought — it's monitored with the same rigor as spending.

Since **1 category (Uncategorised) is already 314% over its budget limit** while total money out is close to eating the entire month's income, the main opportunity here is tightening categorization of transactions and reining in whichever spending is currently falling into "Uncategorised."

### Steps followed

- Step 1 : Exported the bank statement (Capitec account) covering **1 April 2026 – 13 May 2026** and loaded all 73 transactions into a **Transactions** sheet with columns: `Date`, `Description`, `Type`, `Money In (R)`, `Category`, `Fee (R)`, `Money Out (R)`, `Balance (R)`, `Budget Limit (R)`, `Status`.
- Step 2 : Built a **Lookup** sheet mapping each spending `Category` to its monthly `Limit` (e.g. Takeaways = R1,500, Groceries = R800, Cellphone = R800, Fuel = R300), used as the single source of truth for budget limits.
- Step 3 : Used **XLOOKUP** on the Transactions sheet to pull each transaction's `Budget Limit (R)` live from the Lookup sheet based on its `Category`, and to compute a `Status` flag (e.g. "✅ Under Budget") per row.
- Step 4 : Built a **Categories** sheet summarizing `Monthly Limit (R)` vs. `Actual Spend (R)` per category, so total spend per category could be compared to budget at a glance.
- Step 5 : Built a **Savings** sheet tracking 5 goals — `Goal`, `Target (R)`, `Current (R)`, `Remaining (R)`, and `Progress %` — for Laptop, Vacation, Emergency Fund, New Phone, and Books/Study.
- Step 6 : Built the **Dashboard** sheet as the summary front page:
  - Account Overview cards: Opening Balance, Closing Balance, Available Balance
  - Money In vs. Money Out (excl. fees) summary
  - A "Spending Analysis by Category" table, pulled live from Transactions via XLOOKUP, showing Spent, Limit, Remaining, % Used, and Status per category.

## Insights

### Account Overview

- Opening Balance: **R2,055.25**
- Closing Balance: **R1,932.72**
- Available Balance: **R1,770.72**
- Statement period: **1 April 2026 – 13 May 2026** (73 transactions)

### Money In vs. Money Out

- Total Money In: **R5,500.13**
- Total Money Out (excl. fees): **R5,431.38**
- Total Fees paid: **R191.28**

  thus, money out (plus fees) came very close to matching money in for the period — there was almost no net surplus left over after fees.

### Spending by Category (Top 5 by actual spend)

1. Uncategorised — R1,570.00 (limit R500 → **314% used, over budget**)
2. Takeaways — R1,015.50 (limit R1,500 → 67.7% used)
3. Cellphone — R660.00 (limit R800 → 82.5% used)
4. Gifts — R495.00 (limit R500 → 99.0% used, right at the limit)
5. Public Transport — R382.00 (limit R600 → 63.7% used)

  thus, the only category actually over budget is **Uncategorised**, which suggests some transactions need to be re-tagged into a proper category — everything else tracked stayed within its limit.

### Lowest-Spend Categories

- Fuel — R20.50 (6.8% of R300 limit used)
- Personal Care — R29.99 (15.0% of R200 limit used)
- Groceries — R113.50 (14.2% of R800 limit used)

  thus, transport (fuel), personal care, and groceries were the most under-utilized budget categories this period.

### Savings Progress

| Goal | Target (R) | Current (R) | Progress % |
|---|---|---|---|
| Laptop | 15,000 | 4,000 | 26.7% |
| Vacation | 8,000 | 2,000 | 25.0% |
| Emergency Fund | 10,000 | 3,500 | 35.0% |
| New Phone | 5,000 | 1,200 | 24.0% |
| Books/Study | 3,000 | 900 | 30.0% |

- Total saved across all goals: **R11,600** out of a combined target of **R41,000** (**28.3% overall progress**)
- thus, the **Emergency Fund** is furthest along proportionally (35%), while **New Phone** is the furthest behind (24%).

## Tech Stack

- Microsoft Excel
- XLOOKUP (live category-limit lookups)
- Formula-driven dashboard (no external BI tool)
