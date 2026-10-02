# Codex review: known mistakes and unresolved questions

**Reviewer: Codex. Status as of October 2, 2026: open; no research fixes applied.**

I asked Codex to review my thesis materials and document its findings while preserving my original work. The findings below separate observed errors from questions requiring further investigation. My next task is to fix the errors, resolve the version questions, and assess their effect on the conclusions.

The earlier review was static, dated September 15, 2026. Selected evidence was rechecked when this archive was prepared on October 2. The notebooks were not executed. Cell numbers below count **all cells from one**, including Markdown cells; they are not notebook execution numbers.

## 1. Incomplete statement extraction — confirmed error

**Evidence:** [notebook 03](notebooks/03_statement_tone_and_regressions.ipynb), cell 9, `START_MARKERS` and `extract_statement_text`.

The parser starts at the first line matching a short list of phrases. When an opening paragraph uses a different phrase, it can start at a later paragraph and silently omit substantive content. Codex's earlier review reported truncation in **16 of 78 statements**, and media-inquiry boilerplate in **26 extracted files**. Those full counts are carried forward from that review; they were not independently recounted during packaging.

The March 16, 2022 example was rechecked in the selected historical copy: `data/processed/fomc_statements_text/20220316.txt` begins at the Committee's objectives paragraph, while the cached HTML also contains preceding economic-conditions and Ukraine paragraphs. The local raw/extracted files are not bundled in this archive.

**Implication:** dictionary and FinBERT features use incomplete or contaminated input. The magnitude, significance, and interpretation of the reported tone relationship require re-evaluation. This finding does not establish in advance whether corrected results will strengthen, weaken, or reverse it.

**My planned fix:** repair extraction, audit all event documents against their sources, define treatment of administrative/voting text, and regenerate every dependent feature, regression, and table.

## 2. Competing snapshots and stale labels — confirmed inconsistency; cause unresolved

**Evidence:** this archive's [summary table](reports/tables/vrp_summary_stats.csv) reports **2,492** observations, matching the submitted thesis. A later local working version reports **2,454**. The earlier review also found different hashes for the raw FRED snapshot and four processed parquet files across those versions.

[Notebook 01](notebooks/01_build_vix_vrp.ipynb), cell 7, requests data through `2026-02-05` but writes a file named `fred_sp500_vix_vintage_2026-02-04.parquet`. The code downloads and overwrites that file rather than reading a fixed historical snapshot. A fixed requested date range is not enough to guarantee unchanged input data.

**Implication:** a reproducible match between the final thesis and the available code/data has not been established. Matching counts alone do not resolve the discrepancy, and this archive does not identify which snapshot is correct by assumption.

**My planned fix:** compare dates, values, event membership, missingness, and transformations; document which state produced the submitted results; separate frozen historical replication from a new-data refresh.

## 3. Project-root discovery can leave the project — confirmed code defect

**Evidence:** notebooks `02`–`05`, cell 3, ascend directories until they find `.git`, then change the working directory. If a downloaded ZIP has no `.git`, this can reach a drive/root directory or an unrelated enclosing repository.

**My planned fix:** use an explicit project location or stable project marker, and fail clearly when required inputs are missing. The original code remains unchanged here.

## 4. Incomplete and machine-specific environment — confirmed reproducibility gap

**Evidence:** [environment.yml](environment.yml) retains a personal Windows prefix and mostly unpinned dependencies. It does not explicitly include `torch` or `transformers`, imported in [notebook 05](notebooks/05_finbert_tone.ipynb), cell 7. That cell names `yiyanghkust/finbert-tone` without an immutable model revision.

**My planned fix:** create and test a complete portable environment, pin relevant dependencies and the model revision, and document the required inputs. The original environment file is retained byte-for-byte.

## 5. Proposal-era claims exceed the implementation — confirmed documentation mismatch

**Evidence:** the [original README](archive/README.original.md) promises an option-chain/model-free-variance pipeline and an estimator comparison. The submitted implementation instead uses `(VIX / 100)^2` as an implied-variance proxy. The proposed option-chain estimator comparison was not completed.

**Treatment in this release:** the new introductory documentation states the implemented scope and retains the old README as an explicitly labeled historical artifact. No missing estimator has been implemented and no analysis has been changed.

## 6. Interpretation and trading use — limitations, not automatically coding errors

The forward realized-variance term is known only later. Full-sample standardization and PCA in [notebook 02](notebooks/02_fomc_event_study.ipynb), cell 17, are retrospective. Leave-one-out refits assess influence rather than chronological predictive performance. These features do not by themselves invalidate a descriptive study, but they prevent treating its reported associations as evidence of a live trading signal.

**My planned extension:** after correcting the research, consider a separate trading-strategy study with properly timed information and out-of-sample evaluation. Neither a profitable strategy nor its absence has been demonstrated here. See [NEXT_STEPS.md](NEXT_STEPS.md).

## Review limits

Codex identified several mistakes; this is not an exhaustive audit or a clean bill of health for unmentioned components. Packaging checks establish that files were preserved, not that estimates are correct. Saved outputs and the submitted PDF are historical evidence, not freshly reproduced results. I will close findings only after implementing and validating the corresponding corrections.
