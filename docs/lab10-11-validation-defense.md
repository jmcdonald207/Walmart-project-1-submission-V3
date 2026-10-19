# Project 1 — Lab 10 and 11 validation defense

**Evidence status:** Analytic checks and program-observed checks, not a student-authored precommitted prediction. Uses [existing model](../models/walmart_project1.py), [Lab 11 rerunner](../models/walmart_sensitivity.py), [Lab 10 pro forma](../models/walmart_proforma.py), and [GitHub Actions successful run 39178101348](https://github.com/jmcdonald207/Walmart-Project-1-Submission/actions/runs/39178101348). Financial values below are **provisional, assumption-driven model outputs**, not fully sourced fair values.

## Lab 10: Three-statement forecasting and internal integrity

The FY2027–FY2031 projection derives income statement operating income, working-capital needs and cash generation from five-year drivers. A balance-sheet identity alone does **not** establish that the inputs are sourced properly; the model also calculates cash from prior ending cash plus modeled cash movements.

Tests already implemented in `models/walmart_project1.py`:
1. Five projected annual balance-sheet gaps must each equal zero within numerical tolerance.
2. Each year's closing cash must independently tie to the previous year's cash plus modeled FCFE minus shareholder distributions plus revolving-credit draws minus repayments.
3. Injecting a **$10 million artificial balance-sheet gap** must cause an AssertionError. This is a deliberate negative test, not an accounting transaction.
4. An invalid terminal growth rate equal to WACC causes a ValueError, rather than a nonsensical valuation.

**Actual run evidence:** all those checks passed on October 18, 2026. See [visible-output transcript](../outputs/visible-output.md). FY2031 base EBIT **$35,310.09 million**; derived FY2027–2031 FCFF **$10,941.00, $12,565.88, $14,079.05, $15,641.23, and $17,072.93 million**. Numbers reflect the entered forecasts and cannot establish future performance.

**Analytical mechanism:** `FCFF_t = FCFE_t + scheduled debt principal repaid_t + interest_t(1 - model tax rate_t)` for this particular implementation, because revolving draws/repayments are tracked separately from the FCFE series. Verify the financing definition before calling this a general GAAP-to-FCFF transformation; finance leases and noncontrolling interest are not fully reconciled.

## Lab 11: Changed assumption / sensitivity defense

`models/walmart_sensitivity.py` changes **one input driver at a time** from the same base forecast:
- Gross margin is reduced/increased by **0.005 absolute decimal units** (0.5 percentage points) in each of five years.
- SG&A divided by gross profit is reduced/increased by **0.01 absolute decimal units** (1 percentage point) in each year. Since it is a *ratio to gross profit* rather than revenue, a lower SG&A ratio should, other things equal, raise operating income.
- For each perturbation the script reprojects statements, checks every annual cash and balance tie, measures differences in terminal-year EBIT, FCFE and the *FCFE-model* share-value proxy, then restores the original baseline and checks that restored outputs match exactly (within numerical tolerance).

**Causal rationale:** Raising gross margin, with sales and other drivers held fixed, increases gross profit and generally improves operating income/cash flows. Raising SG&A *as a fraction of gross profit* reduces profit and generally reduces equity value. **These are testable expected directions, not recorded predictions made by the student before execution.** Numeric outputs should be captured from a fresh `python models/walmart_sensitivity.py` run if they are presented as observed Lab 11 results.

**Do not confuse valuation methods:** Lab 11's `model.value(rows)` is an **FCFE discounted at cost of equity**, while the integrated `models/walmart_project1.py` discounts **FCFF at WACC** and uses a provisional EV-to-equity bridge. The historical `analysis/what_if_sensitivity.md` predates the current pro forma assumptions and **must not be used as if it shares the same baseline**. Neither sensitivity sequence alone proves the true market valuation.

## DCF robustness: observed low/base/high and discount sensitivity

From [actual logged output](../outputs/visible-output.md), the integrated FCFF model reports:

| Case | Per-share proxy | FY2031 EBIT | Terminal-value share |
|---|---:|---:|---:|
| Downside | $16.93 | $27,082.58 mm | 81.35% |
| Base | $33.33 | $35,310.09 mm | 81.32% |
| Upside | $42.76 | $40,243.18 mm | 81.52% |

At **2.5% terminal growth**, increasing WACC from **6.5% to 7.5% to 8.5%** changes the base valuation proxy from **$43.01 to $33.33 to $26.89**. That is a material $16.12/share spread, showing that cost of capital is a load-bearing assumption. Raising terminal growth from **1.5% to 3.5% at 7.5% WACC** increases the proxy from **$27.99 to $41.35**. An approximately **81% terminal-value fraction** means forecast and terminal assumptions dominate the computed enterprise value.

**Interpretation for WATCH / DEFER:** Since assumption sensitivity is large and the WACC, normalized base, EV bridge and peer comparisons are not independently validated, the tests do not justify buying merely because the code executes. They strengthen the conditional case for deferring until verification; the low/high endpoints are **not a defensible committee valuation interval**.

## Independent numerical / definition checks possible without simulated data

- **DCF arithmetic:** Base case EV $299,780.90 mm = PV explicit $55,988.88 mm + PV terminal $243,792.02 mm. Provisional equity $265,745.90 mm = EV + $10,727 mm cash - $44,762 mm borrowings. These are independent arithmetic reconciliations of printed results, *not* independent financial source verification.
- **Historical accounting definition:** FY2026 **$44,762 mm funded borrowings** = short-term borrowings $6,596 mm + current long-term debt $3,542 mm + long-term debt $34,624 mm; finance leases **$6,761 mm** are *not* included in this debt proxy. The opening model equity **$105,887 mm** includes **$6,270 mm nonredeemable minority equity**. See [FY2026 source ledger](../project1/historical-evidence-and-normalization.md). EV-to-**common**-equity still needs consistent treatment of all noncontrolling interests, operating and finance leases.
- **Financial distinction:** FY2026 CFO less capex ($41,565 - $26,642 = **$14,923 mm**) is not equivalent to the forecast FCFF series and should not be used as validation of the FCFF model without working-capital, interest, tax and investment-basis reconciliation.

## Reproduction and integrity controls

From the repository root run `python models/walmart_proforma.py`, `python models/walmart_sensitivity.py`, and `python models/walmart_project1.py`. Run a clean environment via [the GitHub Actions workflow](../.github/workflows/test-models.yml); record the workflow commit SHA and compare same-code outputs to [saved model output](../outputs/visible-output.md). Because `walmart_all_models.py` embeds historical model copies, **do not use its snapshot output to validate a changed standalone model without synchronizing it**.

## Requirements that still need genuine firsthand evidence

The professor's **Locked Changed-Input Record** requires the student's own AI-off, timestamped prediction and expected *decision* effect **before** running a selected changed-input test. The supplied AI-written expectations above **do not qualify**. Also pending: a documented independent source check of a material AI-originated claim with a disposition, authentic partner comments if assigned, normalized FY2026 bridge, a calibrated WACC, consistent peers and a final committee valuation range. Record these in [authoritative validation-and-AI-use working file](validation-and-ai-use.md).
