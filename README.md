# Probabilistic Graphical Models of U.S. Senate Roll-Call Voting

CSE 150A/250A final project by **Conditionally Independent Caucus**.

We model the 117th and 118th U.S. Senates (Voteview roll calls, 100 senators each) with three graphical models of increasing expressiveness, all implemented from scratch with NumPy/SciPy:

| Model | Learning | Inference |
|---|---|---|
| M1: latent-class Naive Bayes (hidden coalition type per roll call) | EM | exact, O(KN) |
| M2: Chow-Liu tree Bayesian network | MLE / EM | sum-product belief propagation |
| M3: sparse Ising model | ℓ1-regularized pseudo-likelihood (FISTA) | Gibbs sampling, mean-field, exact enumeration (n=16) |

Experiments: **E1** exact vs. approximate inference, **E2** learning with missing data, **E3** conditional vote prediction plus error analysis, **E4** transfer from the 117th to the 118th Senate.

## Repository layout

```
senate_pgm.ipynb     all code and experiments, with outputs
data/raw/            Voteview CSVs for the 117th and 118th Senates
figures/             figures used in the report (PDF)
results/             every result table (CSV)
report/report.tex    final report (report.pdf is the compiled version)
proposal_v2.tex      project proposal
environment.yml      conda environment
```

## Setup and running

```bash
conda env create -f environment.yml
conda activate cse250

# run everything (about 10 minutes); regenerates figures/ and results/
jupyter nbconvert --to notebook --execute --inplace senate_pgm.ipynb

# build the report
cd report && tectonic report.tex
```

Notebook sections: 1 data, 2 model code, 3 correctness checks against brute force, 4 model selection on a validation split, 5 interpretation, 6 experiments E1–E4, 7 summary tables.

## Data

Lewis, Poole, Rosenthal, Boche, Rudkin and Sonnet, *Voteview: Congressional Roll-Call Votes Database*, <https://voteview.com/>. Files: `S117_*.csv`, `S118_*.csv` (votes, members, rollcalls).

## Working together

- Only one person edits `senate_pgm.ipynb` at a time; say so in the group chat before you start, and commit and push when you're done.
- Pull before you start: `git pull`.
- The report is edited on Overleaf; copy changes back to `report/report.tex` before submission.
- Numbers are frozen on **Nov 21**: no experiment reruns after that date, so the report and notebook stay consistent.
