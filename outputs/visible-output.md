# Walmart Project 1 — Visible executed output

**Source:** Successful GitHub Actions [run 39178101348](https://github.com/jmcdonald207/Walmart-Project-1-Submission/actions/runs/39178101348), executed 2026-10-18 23:49 UTC, on Python 3.11. This file transcribes the actual `python models/walmart_project1.py` output from that run, not a fresh market data pull. Code commit/versions in the workflow log should be retained on freezing.

**Decision:** provisional **WATCH / DEFER** — no existing position. **Valuation status:** illustrative equity-value **proxies**, *not verified common-share prices* or a committee-ready range. Model starting accounts as of Walmart fiscal 2026; historical stock comparison in notes is dated September 9, 2026 and requires independent price verification. Forecast periods: FY2027–FY2031. USD millions unless per-share.

## Actual program results

| Case | FY2031 EBIT | PV explicit FCFF | PV terminal | EV | Cash | Funded debt | Common equity proxy | Per-share proxy | PV terminal / EV |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Downside | 27,082.58 | 31,524.43 | 137,479.99 | 169,004.42 | 10,727 | 44,762 | 134,969.42 | **$16.93** | 81.35% |
| Base | 35,310.09 | 55,988.88 | 243,792.02 | 299,780.90 | 10,727 | 44,762 | 265,745.90 | **$33.33** | 81.32% |
| Upside | 40,243.18 | 69,280.86 | 305,690.45 | 374,971.31 | 10,727 | 44,762 | 340,936.31 | **$42.76** | 81.52% |

**Annual projected FCFF ($mm):** downside 6,048.74; 7,070.94; 7,977.49; 8,882.30; 9,627.82. Base 10,941.00; 12,565.88; 14,079.05; 15,641.23; 17,072.93. Upside 13,383.17; 15,433.68; 17,393.73; 19,448.62; 21,407.72.

## WACC and terminal-growth sensitivity — base case, provisional $/share

| WACC | g=1.5% | g=2.5% | g=3.5% |
|---|---:|---:|---:|
| 6.5% | 34.69 | 43.01 | 56.88 |
| 7.5% | 27.99 | **33.33** | 41.35 |
| 8.5% | 23.21 | 26.89 | 32.04 |

Provisional reverse-DCF result: **+13.7801 percentage points** uniform explicit revenue-growth shift to reach the dated $105.83 example price **under this model's incomplete enterprise-equity bridge**. This is *not* the same as the original September 9, 2026 reverse-FCFF model, whose assumptions and opening inputs differ.

## Actual test evidence

- GitHub Actions ran Python compilation and the original combined runner without failure; `7 script(s) attempted; 0 failure(s)`.
- The standalone integrated script logged **CHECKS PASS**: all five annual balance-sheet and cash ties, WACC and terminal growth monotonicity, invalid terminal-growth failure, and deliberate broken balance-sheet failure.
- Training checks: $27.4974 DCF/share at 10% WACC and approximately $23.41 at 11% WACC; Lab 7 two-peer Asbury P/E range $215.81–$246.18 and middle $231.00.
- **Not covered by the successful code run:** verification of source-to-normalized FY2026 base, all financing and noncontrolling minority claims, WACC calibration, historical peer EV/EBITDA, a real AI-off precommitted prediction, or partner validation.

## Investment interpretation

The high terminal-value fraction (~81%) makes the results highly dependent on the terminal assumptions. Downside business risk includes slower consumer sales growth, margin compression and higher automation capex; the scenario inputs are illustrative analyst choices and not management guidance. These proxies should not be mechanically averaged with P/E estimates or presented as a credible investable range. Given the unresolved bridge and peer evidence, the supported action at this stage remains **WATCH / DEFER pending verification**.
