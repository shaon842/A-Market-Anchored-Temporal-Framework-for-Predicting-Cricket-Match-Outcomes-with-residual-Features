# ODI Cricket Match Prediction Using Market-Anchored XGBoost

## Project Overview

This is a research project focused on predicting One Day International (ODI) cricket match outcomes using machine learning. The main idea is to combine bookmaker odds with historical cricket performance data to make more informed predictions.

Instead of training XGBoost to predict the result completely from scratch, the proposed **Market-Anchored Residual XGBoost** model starts with bookmaker-implied probabilities and learns corrections using cricket-related features. The project also compares different modeling approaches and checks how well the model performs on newer matches.

## Dataset

The project combines two sources of ODI cricket data:

- **Market odds data:** Bookmaker odds, implied win probabilities, market favorite information, and related market features.
- **Historical match data:** Previous team performances, ratings, recent form, head-to-head records, and venue-related information.

The final modeling dataset contains **1,192 usable market rows**, with approximately **93.96% historical-data coverage** reported in the notebook.

## Methodology

The main steps of the project are:

1. Clean and combine market odds and historical match data.
2. Create historical features using only information available before each match.
3. Engineer features such as Elo and Glicko ratings, recent team form, win rates, head-to-head performance, and market-rating differences.
4. Use bookmaker probabilities as the starting point for XGBoost and train the model to learn residual corrections.
5. Compare model variations, including home-team and market-favorite views.
6. Use a chronological train, validation, and test split so the newest matches are kept for final evaluation.
7. Analyze model performance, errors, probability calibration, and feature-group contributions.

The notebook also includes exploratory data analysis, an ablation study, and leakage checks to avoid using match results, final scores, or future-derived statistics as prediction features.

## Results

The primary model achieved the following results on the **held-out chronological test set**:

| Metric | Result |
| --- | ---: |
| Accuracy | **85.36%** |
| ROC-AUC | **90.17%** |
| Brier Score | **0.1234** |
| Validation Accuracy | **84.29%** |

The test matches cover **22 July 2022 to 23 April 2026**. These results are from the saved final experiment documented in the notebook, rather than a new run of the uploaded file.

## Tools and Libraries

- Python
- Pandas and NumPy
- XGBoost (used in the final model described by the notebook)
- Scikit-learn
- Matplotlib
- Jupyter Notebook

## How to Run

The uploaded notebook is a **report and analysis notebook**, not a fully standalone training script. It reads results and datasets produced by the separate final-model pipeline.

1. Keep the report notebook alongside the project's `final version` folder.
2. Make sure the original market-odds and match-history datasets, along with the `final_model_outputs` files, are available.
3. Update the local paths in the notebook's setup cell for your computer.
4. Open the notebook in Jupyter and run the cells in order.
5. Generated figures and tables will be saved in the `report_figures` folder.

**Note:** If only this notebook is uploaded, the complete experiment cannot be reproduced without the supporting datasets, final-model script, and saved output files.

## Limitations

This project focuses on ODI cricket, so the results may not apply directly to T20 or Test matches. It also depends on bookmaker odds being available. Some features, including toss and batting-first information, may only be known after the toss, so the prediction timing needs to be considered when using the model.

## Conclusion

This project shows how bookmaker probabilities and historical cricket statistics can be combined for ODI match prediction. The main contribution is using XGBoost to learn adjustments to market expectations instead of relying only on odds or only on past match performance. Future work could include testing on newer matches and extending the approach to other cricket formats.
