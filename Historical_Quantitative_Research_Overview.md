# Historical Quantitative Research Overview

> **Status: Historical experimental research**
>
> This document summarizes the quantitative trading research preserved in `exploratory-daytrading`. It is a historical research record, not a current system manual, validation certification, profitability claim, or statement of deployment readiness.

The repository captures an exploratory research path across supervised machine learning, reinforcement learning, anomaly detection, clustering, model selection, backtesting, and execution-platform integration. The work is intentionally heterogeneous: different notebooks reflect different stages of research maturity, different evaluation designs, and different experimental goals.

For the repository-level orientation and links to successor projects, see the [README](./README.md).

### How to read this overview

This document follows the research from early exploratory modeling through more
structured evaluation, reinforcement-learning experiments, and execution
prototypes. Readers looking for repository navigation should start with the
README; this overview focuses on methodology, representative results, and the
lessons that shaped the later research platforms.

## 1. Historical Research Overview

The research began with feature engineering and supervised classification on hourly equity data, then expanded into multi-stock experiments, chronological testing, rolling date-window studies, anomaly detection, clustering, cross-model comparison, reinforcement learning, and execution-platform prototypes.

Much of the work used public market data downloaded with `yfinance`, including 1-hour bars and multi-ticker datasets. Feature sets included combinations of moving averages, volatility measures, Bollinger-style bands, RSI, MACD, stochastic indicators, OBV, CCI, rate-of-change features, and other price-derived signals. The archive also contains explicit attempts to remove known leakage-style signal columns from feature sets during early experimentation.

The research later broadened beyond classical ML to include Random Forest, XGBoost, LightGBM, KMeans, Isolation Forest, One-Class SVM, autoencoders, PPO, SAC, TD3, A2C, DQN, and related experimental variants. These models were not evaluated under one uniform protocol, so their preserved results should be read within the methodology of the notebook that produced them.

## 2. Research Progression

### Early feature engineering and supervised ML

[`Feature_Engineering_Trading.ipynb`](./Feature_Engineering_Trading.ipynb) represents an early single-stock research stage. It builds technical features, removes several explicitly identified leakage columns, and tests Random Forest classification. The notebook contains more than one evaluation approach: one stage uses a chronological 70/30 split, while a later cuML Random Forest stage uses a random train/test split.

[`Multi_Stock_Feature_Engineering_Trading.ipynb`](./Multi_Stock_Feature_Engineering_Trading.ipynb) extends the same general feature-engineering approach to a multi-stock dataset and continues Random Forest experimentation using a random train/test split.

### Multi-stock classical ML and chronological testing

The archive then moves toward larger multi-ticker studies and time-aware evaluation. [`multi_ticker_LightGBN_walkforward.ipynb`](./multi_ticker_LightGBN_walkforward.ipynb) evaluates LightGBM across a 53-ticker universe using a chronological split with `shuffle=False`. Despite the historical filename, the preserved training cell is a fixed chronological 80/20 train/test experiment rather than a repeated rolling walk-forward procedure.

[`multi_stock_XGBoost_rf_walkforward.ipynb`](./multi_stock_XGBoost_rf_walkforward.ipynb) similarly uses explicit calendar periods, including a 2022 training interval and a 2023 testing interval for Random Forest and XGBoost experiments. This marks a clear shift from random splitting toward date-based evaluation.

### Rolling date-window experimentation

[`XGBoost_rf_walkforward_results_v3.ipynb`](./XGBoost_rf_walkforward_results_v3.ipynb) contains a genuine rolling date-window implementation. Its window generator advances through approximately 365-day training periods, 60-day test periods, and 60-day steps. This is stronger evidence of repeated chronological experimentation than the earlier fixed-split notebooks.

The same notebook also preserves an important research limitation: a later portfolio-simulation stage explicitly replaces model signals with randomly generated signals under a `TEMP DEBUG ONLY` comment. The rolling-window model accuracy output remains useful historical evidence, but portfolio, Sharpe, or drawdown values produced after that signal substitution should not be attributed to the trained model.

### Broader research surfaces

The repository subsequently expands into anomaly detection, clustering, cross-model selection, reinforcement learning, and execution-oriented prototypes. This progression is visible across notebooks such as [`multi_stock_anomaly_pipeline.ipynb`](./multi_stock_anomaly_pipeline.ipynb), [`multi_stock_kmeans_trading_strategy.ipynb`](./multi_stock_kmeans_trading_strategy.ipynb), [`Model_Selector_v1.ipynb`](./Model_Selector_v1.ipynb), [`multi_stock_ppo_training_walkforward.ipynb`](./multi_stock_ppo_training_walkforward.ipynb), [`multistock_td3_results.ipynb`](./multistock_td3_results.ipynb), and [`PPO_Quantconnect_Converted_.ipynb`](./PPO_Quantconnect_Converted_.ipynb).

## 3. Evaluation Methodology

The repository does not use one repository-wide validation design. Several distinct methodologies are preserved:

| Evaluation type | Historical example | Interpretation |
|---|---|---|
| Random train/test split | `Feature_Engineering_Trading.ipynb`, `Multi_Stock_Feature_Engineering_Trading.ipynb` | Early exploratory supervised-ML evaluation. |
| Fixed chronological split | `multi_ticker_LightGBN_walkforward.ipynb` | Train precedes test in time, but the displayed experiment is a single chronological holdout rather than repeated rolling windows. |
| Fixed date-based train/test | `multi_stock_XGBoost_rf_walkforward.ipynb` | Explicit calendar training and testing periods, including 2022 train / 2023 test experiments. |
| Rolling date-window experiment | `XGBoost_rf_walkforward_results_v3.ipynb` | Repeated chronological train/test windows with advancing dates. |
| Repeated-window RL with same-window evaluation | `multi_stock_ppo_training_walkforward.ipynb` | PPO is trained and then evaluated within the same historical data window. |
| Separate chronological RL train/test | `multistock_td3_results.ipynb` | Distinct chronological training and testing datasets/environments. |
| Execution/backtest experiment | `PPO_Quantconnect_Converted_.ipynb` and related integration notebooks | Tests signal handling, execution assumptions, and platform integration rather than model-training validity. |

Because these designs answer different questions, their metrics are not combined here into a single leaderboard. A high classification accuracy from a random split, for example, is not directly comparable with a chronological trading return, a same-window RL result, or an execution-platform backtest.

## 4. Representative Historical Results

The following results are retained because they help explain the research progression. They are not presented as current validated performance claims.

| Research stage | Preserved result | Methodological context |
|---|---|---|
| Early Random Forest feature work | Approximately **99.1% classification accuracy** in a preserved cuML Random Forest run | Random train/test split in a later stage of `Feature_Engineering_Trading.ipynb`; useful as evidence of the early exploratory stage, not as trading-performance evidence. |
| Multi-ticker LightGBM | Test accuracy generally clustered near **50%** across the 53-ticker experiment | Fixed chronological 80/20 split with `shuffle=False`; not a repeated rolling validation result. |
| Date-based RF/XGBoost | Preserved 2022 training / 2023 testing experiments | Fixed chronological calendar split; illustrates the move toward explicit temporal separation. |
| Repeated-window PPO | PPO beat buy-and-hold in **43 of 212 windows (20.28%)** | Repeated-window experiment across 53 tickers; the agent was trained and evaluated within the same historical window. |
| Single-ticker SAC/PPO comparison | SAC: **-12.48% cumulative return, 0.08 Sharpe, 64.38% max drawdown**. PPO: **44.64% cumulative return, 0.22 Sharpe, 37.60% max drawdown** | Preserved exploratory comparison from `aapl_sac_vs_ppo_training_v1.ipynb`; the result illustrates materially different outcomes within RL research rather than a general model ranking. |
| Historical model selector | Random Forest selected for **44 tickers** and PPO for **9 tickers** in the preserved selector output | Composite score combining historical PPO, RF, and KMeans result files; exploratory selector logic rather than a current selection protocol. |

Earlier versions of this overview also included legacy LightGBM and XGBoost headline tables. Because the exact source outputs for those values are not uniquely traceable within the current archive, the tables are not reproduced here.

## 5. Anomaly Detection and Model Selection

### Anomaly detection and clustering

[`multi_stock_anomaly_pipeline.ipynb`](./multi_stock_anomaly_pipeline.ipynb) explores several unsupervised and semi-supervised approaches, including Isolation Forest, One-Class SVM, a PyTorch autoencoder, PCA, t-SNE, and UMAP. The notebook evaluates anomaly-style behavior on AAPL, TSLA, and MSFT using market-derived features such as RSI, MACD, and OBV.

One representative autoencoder output is retained below because it illustrates this research stage directly.

**Figure 1. AAPL price with autoencoder anomalies.** Historical anomaly-detection visualization produced during the multi-stock anomaly research stage; it is an exploratory diagnostic, not a trading-performance result.

![AAPL Price with Autoencoder Anomalies](https://github.com/user-attachments/assets/589c6422-8fac-4798-ae16-48202c232d29)

[`multi_stock_kmeans_trading_strategy.ipynb`](./multi_stock_kmeans_trading_strategy.ipynb) applies KMeans to standardized market features and maps cluster behavior into Buy/Hold/Sell-style interpretations using forward returns. The preserved evidence supports describing KMeans as an exploratory clustering and signal/regime research surface; it does not establish a general predictive-performance claim.

### Cross-model selection

[`Model_Selector_v1.ipynb`](./Model_Selector_v1.ipynb) combines historical PPO, Random Forest, and KMeans result files and applies a composite score based on Sharpe, return, and accuracy. Later selector notebooks, including [`Model_Selector_v4.ipynb`](./Model_Selector_v4.ipynb), add more developed scoring and scaling logic.

Two preserved figures capture this model-comparison stage:

**Figure 2. Sharpe ratio distribution by model.** Historical cross-model comparison visualization. The plotted values come from experiments with different methodologies and should not be interpreted as a single controlled benchmark.

![Sharpe Ratio Distribution per Model](https://github.com/user-attachments/assets/ff63c961-c454-468f-909c-79abd30e6743)

**Figure 3. Top and bottom models by average selector score.** Historical selector output based on the scoring framework used in the model-selection notebooks; it is not a current validated model ranking.

![Top 5 and Bottom 5 Models by Average Score](https://github.com/user-attachments/assets/e169f466-254a-4074-bbe5-b34689d8ed85)

## 6. Reinforcement-Learning Findings

Reinforcement learning became a major experimental branch of the repository, with PPO, SAC, TD3, A2C, DQN, and related variants appearing across the archive. The preserved results are mixed rather than uniformly favorable.

The multi-stock PPO experiment in [`multi_stock_ppo_training_walkforward.ipynb`](./multi_stock_ppo_training_walkforward.ipynb) creates four overlapping windows per ticker across 53 tickers, producing 212 evaluated windows. In the preserved run, PPO outperformed buy-and-hold in 43 windows, or 20.28%. This is useful negative evidence: the experiment did not show broad superiority over the benchmark in the recorded windows.

Its methodology also matters. PPO is trained on each historical window and then evaluated in the same environment/window. The result therefore documents repeated-window RL behavior, not a separate out-of-sample test.

A separate SAC/PPO comparison preserved in [`aapl_sac_vs_ppo_training_v1.ipynb`](./aapl_sac_vs_ppo_training_v1.ipynb) records a weak SAC outcome and a substantially stronger PPO portfolio outcome, while both runs retain meaningful drawdown. Rather than supporting a general claim that one RL algorithm was superior, the notebook illustrates the instability and sensitivity of exploratory RL results.

Later work demonstrates a different evaluation design. [`multistock_td3_results.ipynb`](./multistock_td3_results.ipynb) separates a chronological training period from a later testing period and constructs distinct training and testing environments. This provides evidence that the RL methodology itself evolved during the project.

## 7. Backtesting, Risk, and Execution Experiments

The archive also contains experiments focused less on model training and more on how signals might behave inside a trading or execution environment.

[`PPO_Quantconnect_Converted_.ipynb`](./PPO_Quantconnect_Converted_.ipynb) is a QuantConnect execution-adapter prototype for externally generated signals. The preserved implementation includes:

- external JSON signal consumption;
- signal freshness checks;
- confidence-based position sizing;
- BUY / SELL / HOLD handling;
- explicit slippage and brokerage assumptions;
- order-fill and closed-trade tracking;
- return-history and risk/performance diagnostics.

These features show an effort to move from isolated model output toward execution-aware experimentation. They do not establish validated live-trading readiness. The repository also contains Alpaca-oriented paper-trading and integration notebooks that should be read in the same historical prototype context.

Earlier strategy notebooks also experimented with trade-signal overlays and rule-based visualization. One representative figure is retained below.

**Figure 4. Historical buy/sell signal overlay.** Exploratory signal visualization from the strategy-development stage; it demonstrates how signals were inspected against price history rather than establishing profitable execution.

![Buy/Sell Signal Overlay on Price Chart](https://github.com/user-attachments/assets/5648e09e-8ee9-4b37-8cd0-26ca99173ec1)

Risk and execution concepts appear throughout later experiments, including stop-loss/take-profit logic, position sizing, volatility filters, slippage assumptions, trade cooldowns, and brokerage/execution constraints. These controls improved the realism of some experiments, but they are implementation choices rather than evidence that generalization or protection against overfitting was established.

QuantConnect also produced a historical **"Likely Overfitting"** warning in preserved backtest material. That warning remains part of the research record. The presence of filtering, risk controls, or execution assumptions should not be interpreted as resolving the warning by itself.

## 8. Limitations and Interpretation

Several limitations are important when reading this repository as a historical research record:

- **Evaluation methodology is heterogeneous.** Random splits, fixed chronological tests, rolling date windows, same-window RL evaluation, separate chronological RL tests, and execution backtests all appear in the archive.
- **Historical filenames are not methodological proof.** A notebook name containing terms such as `walkforward`, `deployable`, `live`, or `ready` reflects the research stage or intended purpose at the time; the implementation must be read to determine the actual evaluation design.
- **Some strong early metrics belong to exploratory designs.** The approximately 99.1% Random Forest classification accuracy, for example, comes from a random-split stage and should not be generalized into a trading-performance claim.
- **Mixed and negative evidence is part of the record.** The PPO 43/212 result, weak SAC performance, and other unstable outcomes are retained because they influenced the direction of later work.
- **One rolling RF/XGBoost notebook contains temporary random-signal simulation.** Portfolio metrics created after that substitution are not model-attributable results.
- **Legacy summary tables are not treated as independently verified.** Exact LightGBM/XGBoost headline values previously shown in this overview are not uniquely traceable to preserved notebook outputs in the current archive and are therefore omitted here.
- **Generalization was not established by the historical archive.** Execution constraints, filtering, risk controls, and repeated experiments may improve realism, but they do not by themselves prove protection against overfitting.
- **Deployment readiness was not established.** QuantConnect, Alpaca, external-signal, and paper/live-oriented notebooks document integration research and execution prototypes rather than validated production deployment.
- **The repository is primarily a notebook-based historical workspace.** It should not be interpreted through the obsolete modular project-tree and installation instructions that appeared in earlier versions of this document.

These limitations do not erase the value of the work. They explain what the preserved experiments can and cannot support and show how the research methodology matured over time.

## 9. Transition to Successor Research

The exploratory archive became the starting point for more structured research rather than the endpoint of the project.

1. [`exploratory-daytrading`](https://github.com/racoope70/exploratory-daytrading) preserves the early experiments, notebook outputs, modeling ideas, mixed results, and integration prototypes described here.
2. [`quant-trading-model-validation`](https://github.com/racoope70/quant-trading-model-validation) moved selected work into a more structured validation workflow.
3. [`ppo-trading-pipeline`](https://github.com/racoope70/ppo-trading-pipeline) developed a later modular implementation and execution-oriented pipeline.
4. [`quantitative-trading-research-platform`](https://github.com/racoope70/quantitative-trading-research-platform) is the current canonical research platform and carries the project forward under a more controlled reproducibility and validation framework.

The historical value of this repository is therefore not that every experiment reached the same methodological standard. Its value is that it preserves the sequence of ideas, implementations, outputs, failures, mixed findings, and evaluation changes that informed the later research architecture.
