# Calibrated uncertainty for climate emulators on ClimateBench

A small reproduction and extension study. It asks whether the baseline emulators in ClimateBench give well-calibrated uncertainty, and whether a simple, well-validated method can improve on that.

Status: work in progress. No results yet.

## Question

ClimateBench provides NorESM2 simulation output and baseline machine learning emulators that map emissions and concentrations of CO2, CH4 and aerosols to annual mean climate fields. The baselines are mostly judged on point-prediction error. This project looks at the predictive uncertainty instead:

1. Do the baseline emulators report uncertainty that matches how often they are wrong?
2. How do a Gaussian process and a small neural network ensemble compare on calibration and coverage, in addition to RMSE?
3. Do temperature and precipitation behave differently?

## Data

ClimateBench v1.0, NorESM2 output with the associated forcing data, from Zenodo (DOI 10.5281/zenodo.5196512). The data are not stored in this repository. See `data/README.md` once it exists for download instructions.

## Plan

- [ ] Read the ClimateBench paper, note metrics and baseline weaknesses
- [ ] Download the data and run the provided baseline notebook unchanged
- [ ] Reimplement one baseline in this repository
- [ ] Add a Gaussian process emulator with predictive uncertainty
- [ ] Add a small neural network ensemble
- [ ] Evaluate calibration: coverage against nominal level, reliability diagrams, proper scoring rules
- [ ] Write a short report (3 to 5 pages) stating clearly what is reproduced and what is new

## Repository layout

```
.
├── README.md
├── requirements.txt
├── data/            # download instructions only, no raw data committed
├── notebooks/       # exploration and figures
├── src/             # data loading, models, evaluation
└── report/          # write-up
```

## Scope and limits

This is a reproduction plus a focused extension on one benchmark and one climate model. It does not claim new climate science. Results from an emulator of a single model say little about other models or about real-world projections.

## Reference

Watson-Parris, D., Rao, Y., Olivie, D., Seland, O., Nowack, P., Camps-Valls, G., Stier, P., et al. (2022). ClimateBench v1.0: A benchmark for data-driven climate projections. Journal of Advances in Modeling Earth Systems.

## Author

Syed Sajal Hasan, University of Hamburg
