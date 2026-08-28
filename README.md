# Exploratory Day Trading Research

![Status](https://img.shields.io/badge/status-historical%20research-lightgrey)
![Python](https://img.shields.io/badge/Python-research-blue?logo=python&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-original%20environment-F9AB00?logo=googlecolab&logoColor=white)


> **Status: Historical experimental research workspace**

This repository preserves early-stage quantitative trading research, prototype models, exploratory notebooks, feature-engineering experiments, and selected research outputs. It documents the research path and the evolution of modeling ideas before selected work moved into more structured validation and research platforms.

Notebooks and scripts here are intentionally not fully standardized. Some retain Google Colab setup cells, captured outputs, environment-specific assumptions, and exploratory naming so the development record remains visible.

## Scope

This repository includes:

- Exploratory model development
- Feature-engineering experiments
- Classical machine-learning and reinforcement-learning prototypes
- Early backtesting, walk-forward, signal-generation, and execution-platform experiments
- Learning-stage notebooks and prototype code
- Research outputs retained for development history

The repository should be read as a historical research workspace, not as a current production trading system or a claim of validated trading readiness.

## Start Here

For a representative path through the research, start with these notebooks:

1. [`Feature_Engineering_Trading.ipynb`](./Feature_Engineering_Trading.ipynb) — early feature engineering and GPU-accelerated Random Forest experimentation.
2. [`Multi_Stock_Feature_Engineering_Trading.ipynb`](./Multi_Stock_Feature_Engineering_Trading.ipynb) — extension from single-stock work toward multi-stock feature research.
3. [`XGBoost_rf_walkforward_results_v2.ipynb`](./XGBoost_rf_walkforward_results_v2.ipynb) — Random Forest and XGBoost experimentation in a walk-forward evaluation setting.
4. [`Model_Selector_v4.ipynb`](./Model_Selector_v4.ipynb) — later cross-model scoring and selection logic spanning reinforcement-learning, tree-based, and clustering model families.
5. [`ppo_multi_stock_training_pipeline.ipynb`](./ppo_multi_stock_training_pipeline.ipynb) — multi-equity data and feature pipeline work with chronological train/validation separation supporting later PPO research.
6. [`PPO_Quantconnect_Converted_.ipynb`](./PPO_Quantconnect_Converted_.ipynb) — historical QuantConnect execution-platform experimentation retained as research history, not evidence of validated trading readiness.

These files are representative rather than exhaustive. Older and alternate notebook versions are intentionally retained because they show iteration, failed paths, changing assumptions, and the chronology of the research.

## Research Progression

The work in this repository progressed from individual-stock experiments and feature construction toward multi-stock datasets, broader model-family comparisons, walk-forward evaluation, reinforcement-learning pipelines, model-selection experiments, and execution-platform prototypes.

That progression was exploratory. Results and implementation ideas from this repository were later subjected to more structured validation and model-quality review rather than being treated as automatically deployment-ready.

## Relationship to Successor Repositories

1. **Exploration — this repository**  
   [`exploratory-daytrading`](https://github.com/racoope70/exploratory-daytrading) preserves the early experiments, prototype models, feature engineering, model comparisons, and exploratory results.

2. **Structured validation**  
   [`quant-trading-model-validation`](https://github.com/racoope70/quant-trading-model-validation) moved selected work into a more structured workflow for walk-forward testing, backtesting, and paper-trading evaluation.

3. **Historical implementation work**  
   [`ppo-trading-pipeline`](https://github.com/racoope70/ppo-trading-pipeline) contains a later modular implementation and execution-oriented pipeline. That work was subsequently subjected to stricter model-quality review and is not the current canonical research repository.

4. **Current canonical research platform**  
   [`quantitative-trading-research-platform`](https://github.com/racoope70/quantitative-trading-research-platform) is the current canonical reproducible research platform for the project and carries forward the work under a more controlled validation framework.

## Historical Notebook and Reproducibility Notes

Many notebooks were created in Google Colab and may contain Colab-specific package installation cells, Google Drive paths, captured dependency output, GPU assumptions, and environment-specific metadata. These are historical artifacts and may not run unchanged in a modern local environment.

Stored metrics, warnings, failures, and outputs have not been rerun or rewritten merely for presentation. They should be interpreted in the context of the notebook and the research stage in which they were produced.

Historical filenames containing terms such as `deployable`, `live_inference`, `paper_trading`, or `ready` describe the experimental stage or intended test surface at the time. They should not be interpreted as a current claim that the associated model was validated for live trading.

## Disclaimer

This repository is for research and educational purposes only.

The code, notebooks, results, and models may be incomplete, unvalidated, environment-specific, or unsuitable for live trading.

Nothing in this repository should be interpreted as financial advice or as a recommendation to trade financial instruments.
