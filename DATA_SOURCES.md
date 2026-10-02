# Data and model sources

I credit the original providers below. External raw/processed inputs and model weights are not bundled in this archive. These links identify acquisition sources; they do not guarantee access to the exact historical versions used in my thesis. No downloads or model inference were run for this release.

| Input | Source | Original role / expected local location |
| :--- | :--- | :--- |
| S&P 500 index | [FRED SP500](https://fred.stlouisfed.org/series/SP500), underlying S&P Dow Jones Indices series | Notebook 01 downloads index levels; combined snapshot in `data/raw/fred_sp500_vix_vintage_2026-02-04.parquet` |
| VIX | [FRED VIXCLS](https://fred.stlouisfed.org/series/VIXCLS), underlying Cboe series | Notebook 01 downloads daily VIX and constructs `(VIX/100)^2` |
| Monetary-policy event data | [San Francisco Fed U.S. Monetary Policy Event-Study Database](https://www.frbsf.org/research-and-insights/data-and-indicators/us-monetary-policy-event-study-database/) | `data/raw/USMPD.xlsx`; event selection and futures-rate changes |
| FOMC statements | Federal Reserve Board; URLs constructed in notebook 03 | Cached HTML under `data/raw/fomc_statements_html/`; extracted text under `data/processed/fomc_statements_text/` |
| Dictionary | [Loughran–McDonald Master Dictionary documentation](https://www3.nd.edu/~mcdonald/Word_Lists_files/Documentation/Documentation_LoughranMcDonald_MasterDictionary.pdf) | `data/raw/LM_MasterDictionary.csv`; dictionary tone and uncertainty |
| Pretrained tone model | [yiyanghkust/finbert-tone](https://huggingface.co/yiyanghkust/finbert-tone) | Notebook 05 uses Transformers/PyTorch inference and chunk aggregation; I did not train this model |

The USMPD is documented by Acosta, Ajello, Bauer, Loria, and Miranda-Agrippino, *Financial Market Effects of FOMC Communication: Evidence from a New Event-Study Database*. Its underlying market source includes LSEG Tick History. The `ED1`–`ED4` fields cover Eurodollar/SOFR futures, reflecting the dataset's transition between instruments; they should not be described as one unchanged contract family throughout.

The raw snapshot filename is not proof of its retrieval date. Notebook 01 requests a February 5, 2026 endpoint and writes a filename labeled February 4. FRED's available history and provider revisions can change later downloads. The exact dataset versions must be reconciled before I claim historical reproducibility.

Processed meeting, variance, and tone datasets are created and consumed across notebooks 01–05. In particular, notebook 04's regression section reads `data/processed/meetings_vrp_usmpd_tone.parquet`, produced by notebook 03; running it independently is not a complete no-text workflow.

The archive retains citations in the submitted thesis and original source. Data/model access and redistribution conditions remain those of their providers; this repository does not grant rights to external inputs. I will document the exact acquired versions and permitted distribution scope as part of the future reproducibility work.
