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
- Early backtesting, chronological and rolling/window-based evaluation experiments, signal-generation, and execution-platform experiments
- Learning-stage notebooks and prototype code
- Research outputs retained for development history

The repository should be read as a historical research workspace, not as a current production trading system or a claim of validated trading readiness.

## Start Here

The repository is iterative rather than perfectly linear. For one evidence-based path through the research, start with these notebooks:

1. [`Feature_Engineering_Trading.ipynb`](./Feature_Engineering_Trading.ipynb) — early single-stock feature engineering and GPU-accelerated Random Forest experimentation, with preserved classification output. The historical accuracy result should be read as an exploratory model result, not as validated trading performance.
2. [`Multi_Stock_Feature_Engineering_Trading.ipynb`](./Multi_Stock_Feature_Engineering_Trading.ipynb) — expansion from single-stock work to a large multi-stock labeled dataset and Random Forest experimentation. Its preserved outputs show the scale-up in data and modeling, while its random train/test split reflects the exploratory standard used at that stage.
3. [`multi_stock_XGBoost_rf_walkforward.ipynb`](./multi_stock_XGBoost_rf_walkforward.ipynb) — multi-stock Random Forest and XGBoost evaluation using a chronological 2022 training period and 2023 testing period, with preserved accuracy, return, Sharpe, portfolio-value results, and comparison plots. Despite the historical filename, this representative run is a fixed chronological train/test experiment rather than the later rolling-window validation standard.
4. [`Model_Selector_v1.ipynb`](./Model_Selector_v1.ipynb) — an executed historical cross-model selector combining PPO, Random Forest, and KMeans result files. It preserves the combined results, per-ticker model selections, a top-results table, and plots; the simple composite score is exploratory and should not be interpreted as the current model-selection protocol.
5. [`multi_stock_ppo_training_walkforward.ipynb`](./multi_stock_ppo_training_walkforward.ipynb) — multi-stock PPO training across repeated data windows with stored portfolio, Sharpe, drawdown, and buy-and-hold comparisons. The preserved result is mixed/negative—PPO wins only a minority of the recorded windows—which is retained because it documents evidence that informed later research. The notebook evaluates the trained agent within the same historical window used for training, so it is not equivalent to the later out-of-sample validation standard.
6. [`PPO_Quantconnect_Converted_.ipynb`](./PPO_Quantconnect_Converted_.ipynb) — historical QuantConnect execution-platform integration for externally generated signals, including signal freshness checks, position sizing, slippage assumptions, and execution metrics. It is an execution-adapter experiment rather than PPO training or evidence of validated live-trading readiness.

These files are representative rather than exhaustive. Older and alternate notebook versions are intentionally retained because they show iteration, failed paths, changing assumptions, and the chronology of the research.

## Research Progression

The historical work is not perfectly linear, but the notebook evidence supports a broad progression from single-stock feature/model experimentation to multi-stock research, classical-model evaluation, cross-model comparison, PPO reinforcement-learning experiments, and execution-platform prototypes.

Evaluation practices also evolved unevenly. Some early notebooks use random train/test splits, some use fixed chronological splits, and later exploratory notebooks use repeated windows. Those historical experiments should not be retroactively described as meeting the stricter validation standard adopted in the successor research repositories.

Results and implementation ideas from this repository were later subjected to more structured validation and model-quality review rather than being treated as automatically deployment-ready.

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

Historical filenames containing terms such as `deployable`, `live_inference`, `paper_trading`, `walkforward`, or `ready` describe the experimental stage or intended test surface at the time. They should not be interpreted as a current claim that the associated model was validated for live trading or that the notebook necessarily implements the current validation definition of that term.

## Disclaimer

This repository is for research and educational purposes only.

The code, notebooks, results, and models may be incomplete, unvalidated, environment-specific, or unsuitable for live trading.

Nothing in this repository should be interpreted as financial advice or as a recommendation to trade financial instruments.
