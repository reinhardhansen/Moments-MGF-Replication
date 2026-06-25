# Moments by Integrating the Moment-Generating Function — Replication

Replication code for the paper **"Moments by Integrating the Moment-Generating Function"** by
Peter Reinhard Hansen and Chen Tong.

A single Julia/Jupyter notebook reproduces every figure and table in the paper and its
Supplementary Material, in the order they appear.

Paper: [arXiv:2410.23587](https://arxiv.org/abs/2410.23587)

## Abstract

> We introduce a general integral framework for computing model-implied fractional, complex,
> absolute, and logarithmic moments from the moment-generating function (MGF), with particular
> relevance for transform-specified econometric models. By evaluating a complex extension of the
> MGF along suitable paths, we obtain exact integral expressions that bypass the need for explicit
> probability densities and high-order derivatives. We establish conditions for negative fractional
> moments using the symmetric Cauchy principal value, including the requirement that the
> distribution have no point mass at the centering point. We demonstrate the theoretical scope and
> computational practicality of the framework through applications to the normal-inverse Gaussian
> distribution and a semicontinuous compound Poisson-Gamma distribution. In the latter case, the
> framework handles point masses at the boundary by evaluating conditional fractional moments.

## Repository contents

| File | Description |
|---|---|
| `ReplicationCodeMomentsIntegrateMGF.ipynb` | Main replication notebook (run top to bottom) |
| `ReplicationCodeMomentsIntegrateMGF.pdf` | Executed notebook with all figures and numerical output |
| figures/ | Individual figure PDFs (Figs 1–3, S.2) |
| `paper.pdf` | Compiled manuscript |
| `supplement.pdf` | Compiled Supplementary Material |
| `Project.toml`, `Manifest.toml` | Pinned Julia environment for exact reproduction |
| `LICENSE` | License terms |

No external data are required — every result is computed from closed-form expressions or simulated
within the notebook.

## Requirements

- **Julia 1.12** (results produced with 1.12.6)
- **Jupyter** with the [IJulia](https://github.com/JuliaLang/IJulia.jl) kernel

The notebook was run with the following package versions (pinned in `Manifest.toml`):

| Package | Version |
|---|---|
| Distributions | 0.25.127 |
| Plots | 1.41.6 |
| QuadGK | 2.11.3 |
| SpecialFunctions | 2.8.0 |
| ForwardDiff | 1.4.1 |
| BenchmarkTools | 1.8.0 |

## How to run

```julia
# from the repository root
julia> using Pkg
julia> Pkg.activate(".")
julia> Pkg.instantiate()     # installs the exact pinned environment
```

Then launch Jupyter and open `ReplicationCodeMomentsIntegrateMGF.ipynb`, or run it headless:

```bash
jupyter nbconvert --to notebook --execute ReplicationCodeMomentsIntegrateMGF.ipynb
```

Run the cells in order; each section is self-contained given the function definitions at the top.

## What reproduces what

| Notebook section | Paper item | Description |
|---|---|---|
| Figure 1 | Fig. 1 | NIG densities and the complex-MGF contour $t\mapsto M_X(1+it)$ |
| Figure 2 | Fig. 2 | NIG absolute moments $\mathbb{E}\lvert X\rvert^{r}$ vs. simulation, with accurate-decimals panel |
| Figure 3 | Fig. 3 | Conditional fractional moments $\mathbb{E}[X^{r}\mid X>0]$ of two compound Poisson-Gamma laws |
| Supplement figure | NIG integrands | CMGF vs. density integrand profiles |
| Table 1 | Timing table | CMGF / derivative / density / simulation timings for $\mathbb{E}\lvert X\rvert^{r}$, $X\sim$ NIG |
| Table 2 | $\chi^2_8$ check | Parabolic-representation verification against closed-form moments |

## Reproducibility notes

- The notebook sets `Random.seed!(2026)` so the Monte Carlo panels are reproducible.
- All timings were measured **single-threaded** on an Apple M2 Max (macOS, `arm64-apple-darwin24`);
  absolute times will differ by machine, but the relative comparisons are stable.
- **Runtime warning:** the right panel of Figure 2 uses `K = 100` (i.e. `N = 10^8` draws per `r`,
  rescaled by `sqrt(K)`), which is several billion draws and can take many minutes. Lower `K`
  (e.g. `K = 1` or `10`) for a fast pass — the curve is only slightly noisier.

## Citation

If you use this code, please cite the paper:

```bibtex
@article{HansenTong:MomentsMGF,
  title         = {Moments by Integrating the Moment-Generating Function},
  author        = {Hansen, Peter Reinhard and Tong, Chen},
  year          = {2024},
  eprint        = {2410.23587},
  archivePrefix = {arXiv},
  url           = {https://arxiv.org/abs/2410.23587}
}
```

## License

See [`LICENSE`](LICENSE). Code is released for replication and reuse; please cite the paper.
