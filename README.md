# Functional temporal diversity in the fly reflects natural motion statistics

**Luisa Ramirez, Julijana Gjorgjieva, Marion Silies**

This repository contains the analysis code accompanying the manuscript *"Functional temporal diversity in the fly reflects natural motion statistics"*. The code reproduces the analytical and simulation results linking temporal diversity in fly visual circuits to efficient coding of natural motion statistics.

---

## Repository structure

```
GITHUB/
├── Filter_notebook.ipynb
├── Filters_PCA.ipynb
├── Stimulus_notebook.ipynb
├── LaminaMedulla_circuits.ipynb
├── NatMovies_LaminaMedulla.ipynb
└── Figures/
```

---

## Notebooks

### `Filter_notebook.ipynb`
**Temporal filter characterization — motion and non-motion pathways** (Figs. 1, S1)

Fits experimental temporal filters of fly visual neurons with the canonical biphasic function (Eq. 6 in the manuscript) for two groups of neurons:

- **Motion detection pathway** — lamina neurons (L1, L2, L3) and medulla ON/OFF neurons (Mi1, Mi9, Tm3, Mi4, Tm1, Tm2, Tm4, Tm9).
- **Outside the motion detection pathway** — a broader set of medulla neurons (Mi2, Tm12, Tm20, Tm34, Tm5b, TmY3, TmY5a, TmY10, TmY14).

For each neuron the notebook plots the experimental trace alongside the fit, computes the mean-square fit error across biphasic filter orders {(3,3), (4,3), (4,4)}, and saves the best-fit parameters. These parameter files are used as input by all other notebooks.

---

### `Filters_PCA.ipynb`
**Principal component analysis of temporal filters** (Figs. 1D–F)

Loads experimental and fitted filter parameters from `Filter_notebook.ipynb` and projects the peak-normalised filters onto a PCA space. Reproduces the two-dimensional feature space (filter area vs. half-life timescale) that captures 97% of the variance across all motion-pathway neurons. Identifies the two main clusters corresponding to single-polarity (monophasic) and double-polarity (biphasic) filter types.

---

### `Stimulus_notebook.ipynb`
**Characterisation of naturalistic stimuli** (Figs. 2C–E)

Generates analytical naturalistic stimuli as a mixture of low-pass exponential filters applied to white noise, band-pass filtered to the ecologically relevant frequency range (1–100 Hz). Key analyses:

- Computes and plots the power spectrum of the naturalistic stimulus and the white-noise input.
- Fits the power-law exponent *k* of the stimulus in log–log frequency space within the experimentally reported range.
- **Slope as a function of timescale** — sweeps the second low-pass filter timescale (τ₂) and records the resulting power-law exponent, producing the τ₂ → *k* mapping used in `LaminaMedulla_circuits.ipynb`.
- **Inverse fitting** — given a target exponent *k*, recovers the corresponding τ₂ via interpolation and verifies the result.

---

### `LaminaMedulla_circuits.ipynb`
**Analytical SNR and temporal diversity in lamina and medulla circuits** (Figs. 1G, 3B–D, S2E)

Core analytical notebook. Implements the efficient-coding framework of Eqs. (9)–(22) to compute the signal-to-noise ratio (SNR) of circuits composed of fly temporal filters, optimised over a linear decoder.

**Section 4 — SNR, N = 2 neurons**
Evaluates all pairwise circuits within each visual layer (Lamina, ON Medulla, OFF Medulla). For each pathway, plots the SNR of all combinations sorted by performance, and produces a combined scatter of SNR versus the temporal diversity coefficient (Eq. 23).

**Section 5 — SNR, N = 3 neurons**
Extends the analysis to all triplet circuits within each pathway. Saves sorted-SNR bar plots and a combined SNR-vs-diversity scatter.

**Section 6 — Temporal diversity (N = 2)**
Displays the normalised diversity coefficient for all pairwise circuits across the three visual layers on a single axis, annotated with neuron-pair labels.

**Section 7 — Sensitivity analysis with power-law slope**
Sweeps τ₂ ∈ [10, 60] ms in steps of 5 ms. For each value:
1. Converts τ₂ to the power-law exponent *k* using the analytical power spectrum from `Stimulus_notebook.ipynb`.
2. Computes SNR vs. diversity for all pairwise circuits in all three pathways.
3. Fits a single pooled linear regression (Lamina + ON Medulla + OFF Medulla combined) and records the slope and Pearson correlation coefficient *r*.

Produces two summary plots as a function of *k*: (i) slope of the linear fit; (ii) Pearson *r*. Also produces a snapshot scatter plot (SNR vs. diversity with linear fit overlay) for τ₂ = 50 ms.
---

### `NatMovies_LaminaMedulla.ipynb`
**Natural-movie simulations** (Figs. 3E–I, S2A–D)

Validates the analytical SNR predictions against luminance traces extracted from natural videos (Chicago Motion Database). Convolves each circuit's temporal filters with one-dimensional luminance traces sampled from 11 natural videos and quantifies encoding quality via the R² of a linear encoding model (1 s causal lag window).

- **Section 4 — N = 2 neurons**: Computes R² for all pairwise lamina and medulla circuits, plots example encoder traces for high- and low-SNR lamina circuits ({L1,L3} vs. {L1,L2}), and shows R² vs. combinations alongside the standard deviation of R² across stimuli as a function of the temporal diversity coefficient.
- **Section 5 — N = 3 neurons**: Repeats all analyses for triplet circuits.

---

## Dependencies

| Package | Role |
|---------|------|
| `numpy` | Numerical computation |
| `scipy` | FFT, optimisation, statistics |
| `matplotlib` | Plotting |
| `pandas` | Data loading (filter data) |
| `sklearn` | PCA (`Filters_PCA.ipynb`) |
| `sympy` | Symbolic filter inversion (`LaminaMedulla_circuits.ipynb`) |

All notebooks were developed with Python 3 and are self-contained given the fly-filter parameter files (`.txt`) in the data directory specified in each notebook's parameters cell.

---

## Data

Experimental temporal filter data are taken from:

> Currier, T. A., Pang, M. M., & Clandinin, T. R. (2023). Visual processing in the fly, from photoreceptors to behavior. *Genetics*, 224(2), iyad064.

The path to the local copy of these files must be set in the **Parameters** cell of each notebook (`path_to_data` / `path_to_data_motion`).

Natural videos used in `NatMovies_LaminaMedulla.ipynb` are from the Chicago Motion Database (https://cmd.rcc.uchicago.edu/).

---

## Citation

If you use this code, please cite:

> Ramirez L., Gjorgjieva J., Silies M. (2025). Functional temporal diversity in the fly reflects natural motion statistics. *bioRxiv*.
