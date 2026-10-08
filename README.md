# PTSD Behavioral Markers: Supplemental Materials

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23224843.svg)](https://doi.org/10.5281/zenodo.23224843)

Supplemental data, analysis reports, and source code for:

> Yang, Y., Jun, D., Welch, B. M., Sylvia, A., Sprunger, J. G., & Girard, J. M. (2026). *A pilot study of visual, vocal, and verbal markers of PTSD* [Manuscript submitted for publication]. Department of Psychology, University of Kansas.

Preprint: https://doi.org/10.5281/zenodo.23245323

**Website:** https://jmgirard.github.io/pilot-ptsd-markers/

## Contents

- `data/` — deidentified behavioral features and model covariates, with a codebook ([data/README.md](data/README.md))
- `analyses/` — rendered analysis reports (HTML, with supporting files in `*_files/`)
- `src/` — Quarto source files (`.qmd`) for each report
- `index.qmd`, `_quarto.yml` — website source
- `docs/` — rendered website (served by GitHub Pages)

## Reproducing the analyses

The verbal, vocal, and visual analyses and the feature descriptives (Table S1)
run entirely on the shared data. With R and the packages loaded at the top of
each report installed (the models use `brms` and `ordbetareg` with the
`cmdstanr` backend), render them from `src/`, e.g.:

```
cd src
quarto render verbal_analyses.qmd
```

Fitted models are cached in `src/fits/` (not tracked), so later renders reuse
them. The reports in `analyses/` were rendered with R 4.6.1, brms 2.23.0,
ordbetareg 0.8, cmdstanr 0.9.0, and CmdStan 2.36.0. Because the models are fit
by MCMC with fixed seeds, a fresh fit with other software versions or on
other hardware reproduces the reported estimates up to Monte Carlo error.

The sample demographics report (Table 1) uses participant-level demographic
and clinical records that are not shared, so it cannot be re-rendered from
this repository; its source is included for transparency.

To publish updated reports, copy each rendered `src/<name>.html` and
`src/<name>_files/` into `analyses/`.

## Rendering the site

```
quarto render
```

## License

- **Code** (the `.qmd` source files in `src/` and the website configuration):
  [MIT License](LICENSE)
- **Content** (rendered reports in `analyses/` and `docs/`, website text, and
  data files): [CC BY 4.0](LICENSE-CC-BY.md)

## Citation

Please cite the article above. The version of these materials cited in the
article is archived on Zenodo as **v1.0.0**
([doi:10.5281/zenodo.23224843](https://doi.org/10.5281/zenodo.23224843)); the
concept DOI [10.5281/zenodo.23224842](https://doi.org/10.5281/zenodo.23224842)
always resolves to the latest archived version. See also
[CITATION.cff](CITATION.cff).
