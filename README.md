# PTSD Behavioral Markers: Supplemental Materials

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23266798.svg)](https://doi.org/10.5281/zenodo.23266798)

Supplemental data, analysis reports, and source code for:

> Yang, Y., Jun, D., Welch, B. M., Sylvia, A., Sprunger, J. G., & Girard, J. M. (2026). *A pilot study of visual, vocal, and verbal markers of PTSD* [Manuscript submitted for publication]. Department of Psychology, University of Kansas.

Preprint: https://doi.org/10.5281/zenodo.23245322

**Website:** https://jmgirard.github.io/pilot-ptsd-markers/

## Contents

- `data/`: deidentified behavioral features and model covariates, with a codebook ([data/README.md](data/README.md))
- `analyses/`: Quarto source files (`.qmd`) for each report
- `_freeze/`: stored output of each report, so the site rebuilds without running any code
- `index.qmd`, `_quarto.yml`: website source
- `docs/`: rendered website (served by GitHub Pages)

## Reproducing the analyses

The verbal, vocal, and visual analyses and the feature descriptives (Table S1)
run entirely on the shared data. Install R and the packages loaded at the top
of each report. The models use `brms` and `ordbetareg` with the `cmdstanr`
backend. Then render one report by name from the repository root:

```
quarto render analyses/verbal_analyses.qmd
```

A render by name always runs the report's code. Fitted models are cached in
`analyses/fits/` (not tracked), so later renders reuse them. The published
reports were rendered with R 4.6.1, brms 2.23.0, ordbetareg 0.8, cmdstanr
0.9.0, and CmdStan 2.36.0. The models are fit by MCMC with fixed seeds. A
fresh fit with other software versions or on other hardware reproduces the
reported estimates up to Monte Carlo error.

The sample demographics report (Table 1) uses participant-level demographic
and clinical records that are not shared. It cannot be re-rendered from this
repository. Its source is included for transparency.

## Rendering the site

```
quarto render
```

The site uses Quarto's freeze option (`execute: freeze: true`). A full render
uses the stored output in `_freeze/` and does not run the code of a report
that already holds stored output. A report with no stored output runs once,
so it needs its data, its fit files, and R. After every report holds stored
output, a full render needs neither the data nor R.

## Rendering on the data machine

Use the machine that holds the fitted models and the private demographic
records.

1. Move the existing fit files from `src/fits/` into `analyses/fits/`. Make
   sure that `analyses/fits/` holds the same `.rds` files that `src/fits/`
   held. If a fit file is missing, brms refits that model, which takes hours
   and stores new estimates.
2. If the REDCap folder or the participant key is not at the default path in
   `analyses/demographics.qmd`, set `CMBA_REDCAP_DIR` and `CMBA_KEY_FILE`.
3. Run a full render at the repository root:

   ```
   quarto render
   ```

4. Stage only `_freeze/` and `docs/` (`git add _freeze docs`), commit, and
   push the branch.

## License

- **Code** (the `.qmd` source files in `analyses/` and the website
  configuration): [MIT License](LICENSE)
- **Content** (rendered reports in `_freeze/` and `docs/`, website text, and
  data files): [CC BY 4.0](LICENSE-CC-BY.md)

## Citation

Please cite the article above. The version of these materials cited in the
article is archived on Zenodo as **v1.1.0**
([doi:10.5281/zenodo.23266798](https://doi.org/10.5281/zenodo.23266798)); the
concept DOI [10.5281/zenodo.23224842](https://doi.org/10.5281/zenodo.23224842)
always resolves to the latest archived version. See also
[CITATION.cff](CITATION.cff).
