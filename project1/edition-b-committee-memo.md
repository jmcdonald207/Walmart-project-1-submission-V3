# Project 1 — Edition B: Research Evolution (working draft)

**Status: NOT READY FOR COMMITTEE.** This document avoids asserting an unsupported valuation range.

## Decision frame
- User: buy-side portfolio manager with **no existing Walmart position**
- Security: Walmart Inc. common equity (NYSE WMT)
- Horizon: provisional five-year forecast FY2027–FY2031, long-run terminal
- Comparison date: September 9, 2026 for historic market-price baseline; refresh and cite before final submission
- Currency: USD; model financial statements in USD **millions**; per-share result USD
- Share convention: 7,972.4 million shares currently entered in `walmart_proforma.py`; **verify diluted vs actual outstanding share count and fiscal basis**
- Exclusions: no trading costs, portfolio taxes or transaction-control premium; minority interest, leases and other EV claims remain unresolved, not assumed zero

## Original baseline
Preserve the original, unchanged **Project 1 Edition A** and the original Brightspace receipt. Do not regenerate or backdate it. **Pending identification of the actual submitted copy.**

## Business thesis and falsification
Walmart's scale, procurement advantages, grocery exposure and developing high-margin businesses may support resilient cash generation. Contrary evidence could be persistent SG&A deleverage, weakening price competitiveness, lower free cash flow after automation capex or share dilution. See [company research](../walmart-investment-analysis.md). All market claims require dated primary support.

## Historical source map and contamination register
See [historical input ledger](historical-evidence-and-normalization.md). The opening balance sheet contains aggregate plug categories. Cash and debt conventions, minority interest, fiscal-year matching and diluted shares must be independently reconciled before using the output.

## Valuation architecture
1. [Five-year Walmart income statement, balance sheet and cash flow](../models/walmart_proforma.py): assumption-driven **FCFE** forecast.
2. [Integrated FCFF model](../models/walmart_project1.py): derives FCFF from the five-year pro forma, discounts at scenario-independent illustrative WACC, adds terminal value, and bridges enterprise to a **provisional** common equity proxy.
3. [Equity multiple](../models/walmart_peer_pe.py): P/E peers; price and annual EPS require historical corroboration.
4. [EV multiple](../project1/peer-enterprise-multiples.md): EV/EBITDA definition and input register; **EV multiple not calculated until primary inputs are verified**.
5. [Assumption register](../analysis/assumption-challenge-register.md) and [Lab 11 sensitivity](../models/walmart_sensitivity.py).

**Do not average** an unverified enterprise bridge and unverified peer multiples. FCFF is forward-looking and affected by financing normalization; P/E reflects current market beliefs about disparate retail models.

## Scenarios and downside
`models/walmart_project1.py` implements a named illustrative **low/downside** case (lower sales growth and margins, higher SG&A burden, higher capex), base case, and high case, with five-year accounting checks. The downside's recommendation effect cannot be asserted until committee valuation bounds and reference market-price evidence are verified. Current parameter ranges are judgments, **not sourced management guidance**.

## Provisional action: WATCH / DEFER
The fund holds zero Walmart shares. **Do not initiate on an unverified value proxy.** Initiate only if a reconciled FCFF enterprise-equity bridge and at least one corroborating, policy-consistent relative valuation support a margin of safety to a dated market price. Do not initiate if sustained cash conversion falls below downside assumptions or competition materially impairs margin durability.

Monitor: quarterly comparable sales, operating margin, advertising/membership mix, capital expenditure, inventory days, interest-bearing debt, and equity-share changes. The committee should revisit the decision when evidence resolves the NCI/lease/debt bridge and changes the accepted intrinsic-value range.

## Edition A-to-B research evolution

The original authenticated Edition A submission is not available in this repository. The Edition A column below therefore identifies what the existing March 14, 2025 research draft establishes, **not a verified transcription of the frozen Edition A**. Confirm each entry against the unchanged Brightspace-submitted Edition A before freezing this brief.

| Changed item | Edition A — provisional reference, verify against original | Edition B — documented development | Primary driver of change | Evidence or test that justified the change |
|---|---|---|---|---|
| Thesis / recommendation | Initial Walmart research recommends **WATCH–DEFER**; whether this exactly matches Edition A must be confirmed | **WATCH–DEFER** remains provisional, now conditional on enterprise-to-common-equity reconciliation and agreement across defensible valuation methods | Own analysis + AI-assisted modeling | [Original company research](../walmart-investment-analysis.md); [integrated valuation model](../models/walmart_project1.py). **No claim of validated fair value** |
| Data / source choice | Original research used FY2025 Form 10-K and March 14, 2025 information set; verify what Edition A itself included | Newer FY2026 opening model inputs and September 9, 2026 reverse-DCF reference were added; as-of dates remain separate rather than merged | Own analysis + AI-assisted research | [Historical source ledger](historical-evidence-and-normalization.md); [reverse DCF](../analysis/reverse_dcf.md). FY2026 balance and price definitions still require independent source checks |
| Assumption / model design | Original research included a simplified enterprise-to-equity framework; exact Edition A model scope is unverified | Added five-year Walmart three-statement forecasts, pro-forma-driven provisional FCFF DCF, low/base/high cases, sensitivity tests and peer P/E calculations | Course instruction + AI-assisted coding | [Pro forma](../models/walmart_proforma.py); [FCFF model](../models/walmart_project1.py); [peer calculator](../models/walmart_peer_pe.py); [sensitivity](../models/walmart_sensitivity.py). Automated execution demonstrates operation, **not source accuracy** |
| Risk / limitation / uncertainty | Original research identified competitive pressure, margin risk, capex and uncertainty around an attractive entry price | Later models exposed material valuation sensitivity, mismatched historical versus forecast share bases, different lease/debt conventions, and unresolved NCI and EV/EBITDA comparisons | Own analysis + AI-assisted model review | [Assumption challenges](../analysis/assumption-challenge-register.md); [EV multiple definitions](peer-enterprise-multiples.md); [validation record](validation-and-ai-use.md). No actual partner challenge is attributed without a real record |

## What changed from Edition A to Edition B, and why?

The central investment decision has **not demonstrably changed**: the available research supports a provisional WATCH–DEFER position, not an immediate initiation. The analysis has changed in scope and precision of its questions. It progressed from an initial filing-based company assessment toward a five-year operating forecast, a provisional FCFF valuation, comparable-company calculations and sensitivity testing. These additions helped identify which assumptions and definition choices could materially change Walmart's estimated value rather than treating a single output as conclusive.

The work also exposed limitations that matter for the decision: 2025 research and 2026 valuation inputs have different information dates; the common-share denominator and enterprise-to-equity claims need consistent sourcing; and a policy-consistent EV/EBITDA comparison and normalized base are not yet complete. Those uncertainties are why the current analysis does not justify a final numerical committee range. **Before submission, compare this table directly with the original Edition A and revise any provisional statement that does not match the frozen record.**
