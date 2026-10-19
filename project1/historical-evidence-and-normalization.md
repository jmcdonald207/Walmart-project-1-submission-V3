# Historical financial input and normalization ledger

**Status: source check required before final recommendation.** The following are *values used by the Python model*, not all independently verified reported figures. Dollar amounts in millions.

| Model line | Current code value | Required primary-source comparison / normalization |
|---|---:|---|
| FY2026 revenue | 713,163 | Walmart FY2026 Form 10-K consolidated income statements; confirm revenue vs net sales |
| Opening cash | 10,727 | FY2026 balance sheet; verify restrictions and short-term investments |
| Opening inventory | 58,851 | FY2026 balance sheet |
| Opening PP&E | 136,083 | Balance sheet and PP&E note |
| Opening other assets | 79,007 | Model **plug**; replace with named components and check each |
| Accounts payable in 'floor_plan' slot | 63,061 | Verify Walmart payables; rename in a future version for clarity |
| Interest-bearing long debt | 38,166 | Verify current maturities and long-term notes |
| Short-term borrowings ('revolver') | 6,596 | Verify not mistaken for financing facility availability |
| Other liabilities | 70,958 | Model **plug**; replace with mapped reported accounts |
| Total equity including NCI | 105,887 | Reconcile controlling equity and noncontrolling interest separately |
| Diluted shares in valuation | 7,972.4 | Current script describes shares outstanding; **do not claim diluted until verified** |
| Depreciation, capex, working-capital basis | Forecast | Trace cash flow note and normalize historic ratios |

## Week 2 contamination catalog (complete from filings before finalization)

| Potential contamination | Evidence/date/location | Reported amount | Proposed adjustment | Adjusted base | Decision effect |
|---|---|---|---|---|---|
| One-time litigation / restructuring | PENDING | PENDING | PENDING | PENDING | PENDING |
| Gains/losses on investments and disposals | PENDING | PENDING | PENDING | PENDING | PENDING |
| Accounting classification or changed presentation | PENDING | PENDING | PENDING | PENDING | PENDING |
| Period mismatch, currency, unit or diluted/basic share basis | PENDING | PENDING | PENDING | PENDING | PENDING |
| Discontinued business / acquisition effects | PENDING | PENDING | PENDING | PENDING | PENDING |

**Rule:** An unobserved one-time item is not automatically zero. If none exists, cite the reviewed filing note. Freeze the reported → adjustment → normalized mapping and record analyst judgment.


## Source-reconciled FY2026 inputs (added 2026-10-18)

**Primary evidence:** [Walmart FY2026 annual report, consolidated balance sheets (page 54)](https://stock.walmart.com/_assets/_ef4b3350ef1127ae63b1dd51abb6cf31/walmart/db/950/9988/annual_report/Walmart%2B2026%2BAnnual%2BReport.pdf), year ended **January 31, 2026**, USD millions. This independently sources actual opening balance-sheet amounts that appeared as aggregates in the original Python pro forma.

| Model aggregate | Reported components | Sum ($mm) | Code ($mm) | Gap |
|---|---|---:|---:|---:|
| Other assets | Receivables 11,172 + prepaid/other 4,124 + operating lease ROU 14,750 + finance lease ROU 6,123 + goodwill 28,735 + long-term other 14,103 | **79,007** | 79,007 | **0** |
| Other liabilities / other claims | Accrued liabilities 31,187 + accrued income taxes 596 + current operating lease 1,631 + current finance lease 856 + long-term operating lease 13,941 + long-term finance lease 5,905 + deferred taxes/other 16,549 **+ separately presented redeemable noncontrolling interest 293** | **70,958** | 70,958 | **0** |

**Classification caution:** The $293 million of redeemable noncontrolling interest is not ordinary liabilities under the reported presentation. The existing model places it inside an aggregate for arithmetic convenience. This treatment needs a separate common-equity bridge adjustment; the balance-sheet tie is not evidence that the classifications are economically interchangeable.

| Source line, January 31, 2026 | Reported ($mm) | Current opening code | Test |
|---|---:|---:|---|
| Cash and cash equivalents | 10,727 | 10,727 | Equal |
| Inventories | 58,851 | 58,851 | Equal |
| Property and equipment, net | 136,083 | 136,083 | Equal |
| Total assets | 284,668 | 284,668 | Equal |
| Accounts payable | 63,061 | 63,061 (`floor_plan` label) | Equal; rename conceptually |
| Short-term borrowings | 6,596 | 6,596 | Equal |
| Current portion of long-term debt | 3,542 | part of 38,166 | Included |
| Long-term debt | 34,624 | part of 38,166 | Included |
| Walmart shareholders' equity, controlling | 99,617 | Included in total 105,887 | Distinguish ownership |
| Nonredeemable noncontrolling interests | 6,270 | Included in total 105,887 | **Requires EV-to-common-equity handling** |
| Redeemable noncontrolling interests | 293 | in 70,958 aggregate | **Requires separate handling** |

**Debt and lease-definition bridge:** $6,596 + $3,542 + $34,624 = **$44,762 million of borrowings**, as in the code. Separately, finance lease obligations are **$6,761 million**, and operating lease obligations are **$15,572 million**. Source definitions determine whether these are included as financing claims in EV; do not simply include lease debt in EV without harmonizing EBIT/EBITDA, FCFF, and peers.

**Cash-flow historical cross-check:** [FY2026 annual report consolidated cash flow statement](https://www.sec.gov/Archives/edgar/data/104169/000010416926000091/wmtfy26annualreport-final.pdf) reports cash provided by operating activities of **$41,565 million**, and payments for property and equipment of **$26,642 million** in FY2026. Therefore an unadjusted **cash from operations minus capex** reference is **$14,923 million**. This is *not* automatically FCFF; FCFF requires properly measured after-tax financing adjustments, cash-flow conventions and other adjustments. Neither number is a justified normalized base until nonrecurring items are evaluated.

**Normalization decisions still outstanding:** The current code is a forecasting starting point, not an approved *normalized* historical year. Verify unusual gains/losses, restructuring, and classifications through the FY2026 notes, and document accepted adjustments, including a reason for retaining rather than adjusting each material item.
