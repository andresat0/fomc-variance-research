\# Thesis: VRP around FOMC (Surprise vs Tone)



\## Research Question

Does FOMC statement tone/uncertainty explain the variance risk premium (VRP) in SPX options beyond the policy surprise?



\## Core Variable

VRP\_{t,T} = IVAR\_{t,T} - RVAR\_{t->t+T}



\## Key Regressors

\- Surprise\_t: futures-based monetary policy surprise

\- Tone\_t: statement-based tone/uncertainty (dictionary + FinBERT)



\## Deliverables

\- Reproducible pipeline: option chain -> model-free implied variance -> VRP

\- Event dataset: FOMC meetings + surprise + tone + VRP

\- Estimator comparison (math component): baseline vs improved numerical integration/smoothing



\## Timeline

8 weeks: prototype -> full sample -> robustness -> writing



