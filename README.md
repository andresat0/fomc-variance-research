# FOMC News and the S&P 500 Variance Risk Premium

**How do monetary-policy surprises and the language of Federal Reserve announcements relate to the pricing of equity-market uncertainty?** In my Spring 2026 Penn State honors thesis, I study this question around scheduled Federal Open Market Committee (FOMC) statement releases.

My thesis, *Hard News, Soft News, and the S&P 500 Variance Risk Premium on FOMC Statement Days*, is available through **[Penn State University Libraries](https://honors.libraries.psu.edu/catalog/10189ava6461)**. This repository contains the accompanying research notebooks, figures, and tables.

## Research question

FOMC announcements convey both a policy decision and information about the economic outlook. I distinguish between **hard news**, measured through futures-based monetary-policy surprises, and **soft news**, measured through the tone of the accompanying statement. I ask whether statement tone helps explain differences in the meeting-day variance spread beyond the policy-surprise measure and pre-meeting volatility.

I focus on variance because announcements may affect both option-implied uncertainty and the volatility subsequently realized in the equity market. Examining those components separately helps interpret an association in their difference.

## Data and measurement

The submitted study covers **78 scheduled FOMC events during 2016–2025** and **2,492 daily observations** in its variance dataset.

| Component | How I measure it |
| :--- | :--- |
| Implied variance | Daily VIX converted to decimal units and squared: `(VIX / 100)^2` |
| Realized variance | Sum of squared S&P 500 log returns over the next 22 trading days, annualized |
| Variance-spread proxy | Implied variance minus subsequently realized variance |
| Policy surprise | First principal component of four standardized futures-rate changes from the U.S. Monetary Policy Event-Study Database |
| Statement tone | Loughran–McDonald dictionary measures and inference with the pretrained `yiyanghkust/finbert-tone` model |
| Pre-meeting conditions | Lagged implied variance and backward-looking realized variance |

I combine S&P 500 and VIX series from FRED, event and futures data from the San Francisco Fed's USMPD, and Federal Reserve statement text. Provider and model attribution is recorded in [DATA_SOURCES.md](DATA_SOURCES.md).

The variable labeled `vrp` in my code is an **ex-post variance-spread proxy**. Its realized-variance component is observed only afterward; it is not a directly observable event-time risk premium or trading signal.

## Empirical approach

I first construct event profiles from five trading days before to five trading days after each announcement. I then compare the policy-surprise and statement-tone measures in OLS regressions with pre-meeting volatility controls. I use HC1 robust standard errors for meeting-level specifications and HAC(22) inference in the daily specification.

To examine sensitivity, I compare level and change specifications, apply 1% tail winsorization, separate the implied- and realized-variance channels, and assess influential observations using Cook's distance and leave-one-out refits. These exercises investigate the stability and interpretation of the estimated associations.

## Findings reported in the thesis

In the submitted analysis, the conventional policy-surprise and dictionary-tone measures do not explain cross-meeting changes in the meeting-day variance-spread proxy after controlling for pre-meeting volatility. More positive FinBERT statement tone is associated with a lower spread in the reported controlled specification.

These results motivated my interest in whether contextual language measures capture information that simple word counts and futures surprises miss. They are retrospective, in-sample findings; the study does not establish causality or out-of-sample trading performance. The current status of the original estimates is noted below.

## Explore the research

| Material | Contents |
| :--- | :--- |
| [Penn State University Libraries](https://honors.libraries.psu.edu/catalog/10189ava6461) | Full submitted thesis |
| [notebooks/](notebooks) | Original workflow: variance construction, event study, statement measures, regressions, and FinBERT inference |
| [reports/figures/](reports/figures) | Saved variance-series and FOMC event-profile figures |
| [reports/tables/](reports/tables) | Saved summary statistics, regressions, and sensitivity results |
| [DATA_SOURCES.md](DATA_SOURCES.md) | Input sources and dependencies |
| [ARCHIVE.md](ARCHIVE.md) | Historical version selection and preservation details |

## Future research

I would like to explore **testing my assumptions through a trading strategy** after completing the research corrections. A separate study could ask whether statement tone and policy surprises add predictive information for a specified tradable volatility or variance exposure beyond simple volatility and event-calendar baselines.

That extension would use information available at entry, chronological out-of-sample evaluation, realistic execution and transaction costs, and appropriate benchmarks. I have not implemented or backtested a strategy here. My [next-steps plan](NEXT_STEPS.md) describes this possibility in more detail.

## Research status

**The original analysis remains unchanged. Codex's subsequent review found several implementation and documentation mistakes, including incomplete statement extraction, inconsistent data snapshots, and environment/project-path problems.** The text-extraction issue means the reported tone findings need to be reassessed. **My next steps are to fix these issues myself, rerun the analysis, and report any changes to the conclusions.**

Codex helped document these findings and prepare the repository; it did not correct the research. Saved outputs have not been regenerated, and this is not yet a verified, self-contained reproduction package. See [KNOWN_ISSUES.md](KNOWN_ISSUES.md) for the evidence and [NEXT_STEPS.md](NEXT_STEPS.md) for my correction plan.
