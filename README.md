# Functional temporal cell type diversity in *Drosophila* reflects natural motion statistics

Code for the figures of Ramirez, Gjorgjieva & Silies (2026). Each notebook generates the panels of one figure and saves them as PDF in `Pdf_figures/`.

| Notebook | Figure |
|---|---|
| `Fig1_Filters_Clandinindata_PCA_FeatureSpace.ipynb` | Fig. 1C–G |
| `Fig2_Stimulus_PowerLaw.ipynb` | Fig. 2D, E |
| `Fig3_1_SNR_vs_TemporalDiversity.ipynb` | Fig. 3B–F |
| `Fig3_2_NatMovies_LaminaMedulla.ipynb` | Fig. 3G–K, Fig. S4 |
| `Fig4_SNR_GeneralizedFilterSpace.ipynb` | Fig. 4A, C–F, Figs. S5, S6 |
| `Fig5_1_SNR_GeneralizedFilterSpace_Medulla.ipynb` | Fig. 5A, C, D |
| `Fig5_2_LPTC_Silencing_Serbe2016.ipynb` | Fig. 5F, G |
| `FigS2_Triplets_SNR_NatMovies.ipynb` | Fig. S2 |
| `FigS3_SNR_vs_Exponent.ipynb` | Fig. S3 |

## Folders

- `FitParameters/`: parameters of the filter function (Eq. 4) fitted to the measured filters, the 30 filters per cell type, and the filters of the generalized filter space.
- `PrecomputedSNR/`: per-band SNR of the measured circuits. Missing files are recomputed by `Fig3_1_SNR_vs_TemporalDiversity.ipynb`.
- `Data_digitized/`: LPTC responses digitized from Serbe et al., *Neuron* 89 (2016).

## SNR

All functions to compute the SNR (Eqs. 20, 21) are in `Fig3_1_SNR_vs_TemporalDiversity.ipynb`. `snr_circuit` computes the SNR of any circuit (filters, exponent *k*, noise level) and reproduces the precomputed SNR used by the other notebooks.

## External data

The data paths are set in the first code cell of each notebook.

- **Measured filters** (Fig. 1): `ALL_RESPONSES.npy`, Currier & Clandinin, *Cell* 188 (2025).
- **Natural movies** (Figs. 3G–K, S2, S4): ten videos of the Chicago Motion Database (https://cmd.rcc.uchicago.edu/; Salisbury & Palmer, *J. Stat. Phys.* 162 (2016)), from which the luminance traces are extracted (Methods).

## Requirements

Python 3 with numpy, scipy, matplotlib, scikit-learn, pandas and Jupyter. Tested with Python 3.13, numpy 2.1, scipy 1.15, matplotlib 3.10, scikit-learn 1.6.
