# My correction and research plan

I will fix the mistakes Codex identified before relying on the thesis results for new empirical claims. All items below remain future work; this release preserves the original analysis unchanged.

## First: correct and reproduce the study

- [ ] Reconcile the historical and later code/data copies, including their 2,492-versus-2,454 observation counts. Record a chosen snapshot, source dates, checksums, and an explanation of the differences.
- [ ] Repair statement extraction; inspect the full 78-event corpus against original source documents; specify how voting and administrative material are handled.
- [ ] Regenerate dictionary measures and FinBERT inference from the verified corpus, using a recorded model revision.
- [ ] Fix project-root discovery, missing-input handling, and environment dependencies without overwriting the historical archive.
- [ ] Add checks for units, forward-window endpoints, lagged controls, event alignment, merge uniqueness, and PCA inputs/sign conventions.
- [ ] Run the full corrected workflow in a fresh environment and regenerate figures and tables.
- [ ] Compare original and corrected estimates, sample membership, uncertainty, and interpretation. Report unfavorable changes as well as favorable ones.

## Possible extension: test assumptions through a trading strategy

Once the corrections are complete, I may investigate whether the thesis's economic hypotheses have predictive value for a **specified, tradable exposure to equity volatility or variance around FOMC announcements**. This is a research possibility, not a trading recommendation or an implemented strategy.

I would make the hypothesis falsifiable: for example, whether statement tone and policy surprises add information about subsequent outcomes beyond simple volatility and event-calendar baselines. The instrument and forecast target would need to be chosen explicitly; the ex-post spread used in the thesis is not itself a tradable instrument.

Before running that experiment, I would:

1. **Define the information available at entry.** Timestamp statement publication, text processing, surprise-measure availability, and entry prices. A surprise measured over an announcement window cannot be used to place a trade before that window ends. Later realized variance must never enter a contemporaneous signal.
2. **Separate estimation from evaluation.** Use chronological training, validation, and test periods. Fit scaling, PCA, regressions, and any signal thresholds only on past information. Account for overlapping 22-day targets when separating samples, and reserve an evaluation period before tuning the strategy.
3. **Specify implementation.** Choose an instrument, holding period, sizing rule, exit rule, and risk limits. A VIX-based proxy and an actual option, futures, or variance position have different exposures and payoffs; I would model the chosen position directly.
4. **Include realistic costs and execution.** Use executable prices and account for bid–ask spreads, slippage, fees, and financing, hedging, or margin requirements where relevant. Assess liquidity around announcement times.
5. **Compare against simple alternatives.** Evaluate an event-calendar-only rule, a volatility-only rule, and an appropriate passive exposure alongside the proposed signal. Report turnover, drawdowns, tail risk, and performance after costs, not just a favorable average return.
6. **Allow the hypothesis to fail.** Record all tested variants and evaluate stability across time. A profitable backtest would not by itself prove the thesis's economic mechanism; a negative result would still be informative.

I have not implemented, optimized, or backtested a strategy in this repository. Corrected explanatory results and any future trading evaluation will be reported separately from the unchanged submitted thesis.
