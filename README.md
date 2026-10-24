# Calibrated uncertainty for climate emulators on ClimateBench

A small reproduction and extension study. It asks whether the baseline emulators in ClimateBench give well-calibrated uncertainty, and whether a simple, well-validated method can improve on that.

Status: work in progress. No results yet.

## Question

ClimateBench provides NorESM2 simulation output and baseline machine learning emulators that map emissions and concentrations of CO2, CH4 and aerosols to annual mean climate fields. The baselines are mostly judged on point-prediction error. This project looks at the predictive uncertainty instead:

1. Do the baseline emulators report uncertainty that matches how often they are wrong?
2. How do a Gaussian process and a small neural network ensemble compare on calibration and coverage, in addition to RMSE?
3. Do temperature and precipitation behave differently?

## Data

ClimateBench v1.0.0, NorESM2 output with the associated forcing data, created by Duncan Watson-Parris and published on Zenodo (DOI 10.5281/zenodo.7064308, licence CC BY 4.0). The data are not stored in this repository: they are large, and the `data/` folder is ignored by git. To fetch the training/validation and test files (about 0.9 GB):

```
mkdir -p data && cd data
curl -L -o train_val.tar.gz "https://zenodo.org/records/7064308/files/train_val.tar.gz?download=1"
curl -L -o test.tar.gz "https://zenodo.org/records/7064308/files/test.tar.gz?download=1"
md5 train_val.tar.gz test.tar.gz   # macOS; use md5sum on Linux
```

Expected MD5 checksums: `9bf0ebd9662667cc1ed78fd3eb5cad4e` (train_val) and `a09a3ddc8c24e1d6d4b1ee4be5936510` (test). A third file, `CMIP6.zip` (1.5 GB), is also in the record and is not needed unless a later step requires it.

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

Watson-Parris, D. (2021). ClimateBench (v1.0.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.7064308

## Author

Syed Sajal Hasan, University of Hamburg
