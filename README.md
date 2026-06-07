# SIDM-SPARC: Velocity-Dependent Self-Interacting Dark Matter from Rotation Curves

A Bayesian analysis of **124 high-quality galaxy rotation curves** from the
[SPARC database](http://astroweb.cwru.edu/SPARC/), testing a **velocity-dependent
Self-Interacting Dark Matter (SIDM)** cross-section against standard halo models.

> **Paper:** see [`paper/sidm_sparc_paper.pdf`](paper/sidm_sparc_paper.pdf)
> *Reconciling Dwarf and Cluster Constraints on SIDM: Evidence for
> Velocity-Dependent Interactions* — Florian Celli (Independent Researcher).

---

## Summary

Standard ΛCDM struggles on galactic scales (the core–cusp and diversity
problems). SIDM offers a particle-physics solution, but a constant cross-section
cannot satisfy both dwarf galaxies (which need `σ/m ~ 1–10 cm²/g`) and clusters
(which limit `σ/m < 0.1–1 cm²/g`). This work fits a velocity-dependent form

```
σ/m (v) = σ₀ / (1 + (v/v₀)⁴)
```

to the SPARC sample, **marginalising over the stellar mass-to-light ratios**
(a key difference from analyses that fix them).

### Main results

| Quantity | Value |
|---|---|
| Galaxies analysed | 124 (0 failed fits) |
| σ₀ | 3.27 (+0.19 / −0.08) cm²/g |
| v₀ | 34.9 (+0.68 / −0.83) km/s |
| Median reduced χ² (SIDM) | 0.76 |
| Median reduced χ² (NFW) | 1.25 |

Effective cross-section, reparametrised at physical velocities (more robust than
the degenerate `σ₀, v₀` pair):

| v (km/s) | σ/m (cm²/g) |
|---|---|
| 30 | 2.13 |
| 50 | 0.63 |
| 100 | 0.048 |
| 200 | 0.003 |

→ `σ/m ≈ 2 cm²/g` at dwarf scales (enough for core formation), falling steeply
at higher velocities — naturally consistent with cluster upper limits.

> **Honest caveat:** the individual `(σ₀, v₀)` parameters are degenerate (see
> the mock-recovery test in `notebooks/mock_test.ipynb`), and rotation curves
> alone cannot distinguish an SIDM core from a generic cored profile (Burkert
> fits comparably well). Cluster-scale values are an *extrapolation* of the
> fitted form, not a direct constraint from this dataset. The robust result is
> the **shape** of `σ/m(v)` and the preference for a core over an NFW cusp.

---

## Repository structure

```
.
├── paper/
│   └── sidm_sparc_paper.pdf        # the manuscript
├── notebooks/
│   ├── sidm_analysis.ipynb         # main analysis: fits, MCMC, model comparison
│   └── mock_test.ipynb             # method validation (degeneracy recovery test)
├── data/
│   └── sparc/                      # 175 SPARC *_rotmod.dat rotation curves
├── results/
│   ├── sidm_results/               # global fit, MCMC chain, figures, comparison
│   ├── reparametrized_results/     # σ/m(v) constraints + corner plots
│   └── mock_test/                  # mock recovery test outputs
├── requirements.txt
├── LICENSE
└── README.md
```

---

## Reproducing the analysis

```bash
# 1. Create an environment and install dependencies
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt

# 2. Launch Jupyter
jupyter notebook

# 3. Run notebooks/sidm_analysis.ipynb   (main analysis)
#    Run notebooks/mock_test.ipynb       (validation)
```

The rotation-curve files (`data/sparc/*_rotmod.dat`) are read directly by the
notebooks.

> **Note on the code:** the full analysis engine (data loader, SIDM model,
> density profiles NFW/Burkert/DC14/Einasto, scaling relations, global fit and
> MCMC) is defined **inline in `notebooks/sidm_analysis.ipynb`** — the notebooks
> are self-contained. Some cells reference a command-line entry point
> (`sidm_analysis_corrected.py`); that is simply the same code exported as a
> script and is optional — running the notebook cells reproduces everything.

---

## Data attribution

The rotation curves are from the **SPARC** database:

> Lelli, F., McGaugh, S. S., & Schombert, J. M. (2016), *SPARC: Mass Models for
> 175 Disk Galaxies with Spitzer Photometry and Accurate Rotation Curves*,
> AJ, 152, 157.

SPARC data are publicly available at http://astroweb.cwru.edu/SPARC/ and are
included here for reproducibility. All credit for the observations belongs to
the SPARC team.

---

## Citation

If you use this work, please cite the paper (a DOI will be added once archived
on Zenodo):

```
Celli, F. (2025). Reconciling Dwarf and Cluster Constraints on SIDM:
Evidence for Velocity-Dependent Interactions.
```

---

## License

Code and analysis: **MIT License** (see [`LICENSE`](LICENSE)).
SPARC data retain their original terms (see attribution above).
