# Archive selection and preservation

I prepared this public archive on October 2, 2026 with Codex's assistance. My instruction was to preserve my thesis work without fixing its analysis, and to document Codex's findings and the corrections I plan to make.

## Selected sources

- **Submitted document:** available through [Penn State University Libraries](https://honors.libraries.psu.edu/catalog/10189ava6461); the PDF is not included in this repository.
- **Historical computation materials:** `Thesis/Copy of thesis-vrp-fomc/thesis-vrp-fomc`.

The computation copy was selected because its saved summary has 2,492 observations, consistent with the submitted narrative. A later local working tree has a 2,454-observation summary and a different PCA implementation. I did not merge these versions or determine that either one reproduces the thesis exactly. Reconciliation remains my next step.

## Preservation check

All **25 historical files** listed in [ARCHIVE_MANIFEST.json](ARCHIVE_MANIFEST.json) were copied byte-for-byte, including notebook outputs, the environment specification, original ignore rules, five figures, and eleven tables. The proposal-era README was relocated to `archive/README.original.md` without changing its contents. Git attributes disable line-ending conversion for these historical files.

The new root README, issue note, next-steps plan, data-source note, this archive note, manifest, and Git attributes are packaging/documentation additions. No notebook code, saved output, research table, figure, PDF, or environment specification was corrected. No notebook was executed and no result was regenerated. No new research tests were added or represented as passing.

## What this release leaves outside GitHub

The full thesis is linked to its university library record rather than hosted here.

Raw and processed input datasets, model weights, duplicate notebook report directories, old Git history, editor state, drafts, feedback, correspondence, reference-paper PDFs, and unrelated academic files remain outside the public archive. The saved notebooks still contain their original displayed data excerpts and machine-specific paths; these are preserved historical outputs, not a bundled input dataset or portable run configuration.

I have not established redistribution permission for every external input, so those files are not included. Their absence is a stated reproduction limitation, not evidence that the notebooks can run without them. [DATA_SOURCES.md](DATA_SOURCES.md) records the sources and expected roles.

## Historical results

The archived FinBERT tables and thesis conclusions depend on text inputs with known extraction problems. They are retained to make the original work inspectable and support a future original-versus-corrected comparison. They should not be read as corrected findings or verified predictive performance.
