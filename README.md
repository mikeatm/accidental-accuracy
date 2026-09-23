# Accidental Accuracy: exact benchmarks for GW in the extended Hubbard ring

Code and data accompanying:

> M. O. Atambo, *"Accidental accuracy and vertex corrections in GW: Exact
> benchmarks for the extended Hubbard model"*, arXiv:2608.24838
> (preprint; resubmission in progress).

[![arXiv](https://img.shields.io/badge/arXiv-2608.24838-b31b1b.svg)](https://arxiv.org/abs/2608.24838)
[![DOI](https://zenodo.org/badge/1383359668.svg)](https://doi.org/10.5281/zenodo.22918064)

*(Replace the Zenodo badge/link above once the first release is minted —
see "Archiving on Zenodo" below.)*

## What this is

A single self-contained Jupyter notebook, `Finite-extended-hubbard-ring-Accidental-Accuracy.ipynb`,
that:

- Exactly diagonalizes the half-filled extended Hubbard ring,
  `H = -t sum c+_i c_j + U sum n_iu n_id + V sum n_i n_j`, on periodic
  clusters of `N = 6, 10, 14` sites.
- Builds the corresponding model-space static GW / COHSEX theory on the
  identical Hilbert space, so the ED-vs-GW gap difference is a clean
  measure of the GW functional error.
- Extracts the effective scalar vertex `Gamma_eff(U, V)` that makes GW
  reproduce the exact gap, and locates the "accidental accuracy"
  crossover `U*` where standard GW (`Gamma_eff = 1`) is exact.
- Computes the exact dynamical self-energy and spectral function via
  Lehmann representation, to show why gap agreement at `U*` does not
  imply functional accuracy.

Every figure and table in the paper is reproduced by a specific cell —
see the correspondence table below.

## Repository contents

```
.
├── Finite-extended-hubbard-ring-Accidental-Accuracy.ipynb   # the notebook
├── CITATION.cff                                              # citation metadata
└── README.md                                                 # this file
```

## Requirements

Python 3.10+ with:

```
numpy
scipy
matplotlib
```

No GPU, no special hardware. Install with:

```bash
pip install numpy scipy matplotlib jupyter
```

## Running it

Cells are grouped into **common blocks** (imports/style, exact
diagonalization, static GW, Lehmann/self-energy — run these four first)
followed by **section cells**, each self-contained and reproducing one
figure or table. Run top to bottom.

**One cell is expensive**: the `N=14 finite-size extension` cell builds
sparse Hamiltonians of dimension ~11.8M and does 24 Lanczos solves; it
takes on the order of an hour on a laptop. Every other cell finishes in
seconds. If you only want to check the `N=6, 10` results, skip that cell
and the finite-size-scaling cell that follows it (it reads the N=14
cell's cached variables).

## Correspondence to the paper

| Notebook cell | Output | Paper reference |
|---|---|---|
| ED benchmark | printed `E0(N-1), E0(N), E0(N+1)` sweep | data behind Fig. 1 (exact points) |
| COHSEX vs exact | printed gap comparison | data behind Fig. 1 (GW points) |
| Channel-resolved vertex corrections | printed table | data behind Fig. 2 |
| Effective vertex `Gamma_eff(U)` scan | printed table | data behind Fig. 3, Table II (`N=6` column) |
| `V`-sweep crossover points | printed table | Table I (`tab:crossover`) |
| Main-text figures | `fig1_gap.pdf`, `fig2_channel.pdf`, `fig3_gamma_eff.pdf`, `fig4_V_crossover.pdf` | Figs. 1–4 |
| Exact local self-energy | `fig_sigma_exact.pdf` + PH-symmetry validation prints | Fig. 6 (`fig:sigma`) |
| Exact spectral function `A(k,ω)` | `spectral_functions_final.png` | Fig. 5 (`fig:Akw`) |
| Full-frequency G0W0 check | printed table | supports the discussion in Sec. "Limitations"; **known issue** below |
| `N=14` finite-size extension | printed table + `U*(14)` | Table II (`N=14` column), Appendix A |
| Finite-size scaling figure | `fig_scaling.pdf` | Fig. 7 (`fig:scaling`), Appendix A |
| `k`-resolved self-energy at `U=8t` | `fig_sigma_kU8.pdf` | supplementary diagnostic, not in the manuscript figures |

## Known limitation

The full-frequency `G0W0` cell computes a self-energy that is
numerically zero (`Sigma_c ~ 1e-4`) at every `U`, because it convolves a
retarded `G0` with a retarded `W` — both analytic in the upper half
plane, so the frequency integral vanishes by contour closure. A
non-zero result needs the time-ordered `G0` and `W`. This is flagged
in-line in the notebook and in the manuscript; a corrected real-frequency
convolution is left for future work.

## License

Code: MIT (see `CITATION.cff`; add a `LICENSE` file with the MIT text if
one isn't already present in this repository). If you'd rather license
the notebook under something else (e.g. BSD-3 or CC-BY for a
data-heavy release), update the `license` field in `CITATION.cff` to
match.

## Citing this work

See `CITATION.cff` for machine-readable metadata (GitHub and Zenodo
both read this automatically). In short:

- **To cite the code**: cite this repository / its Zenodo DOI.
- **To cite the physics**: cite the paper, arXiv:2608.24838 (preprint;
  update to the published version once available).

## Acknowledgments

The author acknowledges Kenya Education Network (KENET) research
services for computing resources.

## Contact

Michael O. Atambo — michael.atambo@tukenya.ac.ke — Department of
Physics, Earth and Environmental Science, Technical University of
Kenya, Nairobi, Kenya.
