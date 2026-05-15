# PPO + Random Forest Hybrid — Validation Summary

This repo hosts a PPO + Random Forest hybrid trading pipeline for walk-forward validation, backtesting, and paper-trading readiness.  
The model combines a PPO policy for position sizing with a supervised Random Forest gate that filters whether a forecast horizon is actionable before allowing trade exposure.

This version is the **RF-gated baseline**. A separate PPO + XGBoost hybrid should be built later using the same data, features, splits, and evaluation process for a clean model comparison.

---

## What’s new / improvements

1) **Hybrid PPO + RF Architecture**
   - PPO handles continuous position sizing and directional exposure.
   - Random Forest gate estimates trade/no-trade participation before execution.

2) **Multi-Timeframe Dataset**
   - 1-hour bars provide market context features.
   - 15-minute bars provide execution-time features.
   - Context features are merged into execution rows using backward as-of alignment.

3) **No-Lookahead Validation**
   - Future context timestamps are explicitly checked.
   - Exact timestamp matches between context and execution bars are rejected.
   - Context age diagnostics are logged for auditability.

4) **Chronological Validation Split**
   - Per-symbol train/validation split.
   - No random shuffling.
   - Validation data remains later in time than training data.

5) **Random Forest Participation Gate**
   - Binary actionable-horizon label.
   - Class-balanced Random Forest training.
   - Validation threshold sweep for probability cutoff selection.

6) **Artifact & Provenance Tracking**
   - Dataset files, gate model, feature lists, threshold config, validation predictions, and manifest outputs are saved consistently.

7) **Backtest/Paper-Test Readiness**
   - Designed to support PPO-only vs PPO+RF vs PPO+XGBoost comparison.
   - Gate pass/block behavior can be reviewed before live paper-trading promotion.

---

## Minimal pipeline overview

- **Data → Features**: Alpaca OHLCV → 1-hour context features + 15-minute execution features.
- **Merge**: backward as-of merge to prevent future context leakage.
- **Label**: forward-return target and binary gate participation label.
- **Split**: chronological per-symbol train/validation split.
- **Train Gate**: Random Forest classifier on validation-safe features.
- **Validate**: threshold sweep using precision, recall, F1, accuracy, and trade rate.
- **Export**: save gate model, features, threshold, predictions, and manifest records.
- **Compare**: evaluate PPO-only, PPO+RF, and later PPO+XGBoost under the same rules.

---

## Key metrics we track

- Gate Accuracy, Precision, Recall, F1, Confusion Matrix.
- Train/Validation positive rate.
- Validation trade rate by threshold.
- Selected gate probability threshold.
- PPO portfolio value, Buy & Hold comparison, Return, Sharpe, Max Drawdown.
- Trade count, gate pass count, gate block count, gate pass rate.
- Turnover, exposure, skipped decisions, and execution behavior during paper testing.

---

## Saved artifacts

Dataset artifacts:

```text
multi_stock_feature_engineered_dataset_mt.csv
train_mt.csv
val_mt.csv
features_full_mt.parquet
train_mt.parquet
val_mt.parquet
artifact_manifest.json
```

Gate artifacts:

```text
gate_outputs/
  gate_model.joblib
  gate_features.json
  gate_threshold.json
  gate_summary.json
  gate_val_predictions.csv
  gate_threshold_sweep.csv
```

---

## Recommended project structure

```text
ppo-rf-hybrid-validation/
  README.md
  requirements.txt
  .gitignore

  src/
    config.py
    data_download.py
    feature_engineering.py
    leakage_checks.py
    build_dataset.py
    train_gate.py
    validate_gate.py
    manifest.py
    run_validation.py

  data/
    raw/
    processed/

  models/
    ppo/
    gate/

  artifacts/
    manifests/
    features/
    thresholds/

  reports/
    gate/
    backtests/
    paper_trading/
```

---

## Installation & Usage

### Prerequisites

- Python 3.10+
- pip or conda
- Git
- Alpaca market data credentials

### Setup

```bash
git clone https://github.com/racoope70/daytrading-with-ml.git
cd daytrading-with-ml/validation/ppo-rf-hybrid-validation

python3 -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt
```

### Environment variables

```bash
APCA_API_KEY_ID=your_key_here
APCA_API_SECRET_KEY=your_secret_here
```

Do not commit `.env` files or API keys.

---

## Usage

Build or reuse the dataset:

```bash
python src/build_dataset.py
```

Train the RF participation gate:

```bash
python src/train_gate.py
```

Run full validation:

```bash
python src/run_validation.py
```

---

## Validation workflow

1. Build or load the multi-timeframe dataset.
2. Confirm no-lookahead checks pass.
3. Confirm chronological train/validation splits.
4. Train the Random Forest participation gate.
5. Review threshold sweep and gate diagnostics.
6. Save gate artifacts and manifest records.
7. Run PPO + RF backtests.
8. Compare against PPO-only.
9. Promote only stable candidates to paper testing.

---

## RF vs XGBoost comparison plan

This repo is the **PPO + Random Forest baseline**.

The PPO + XGBoost version should be created separately and compared under the same:

- ticker universe
- data source
- feature set
- label definition
- train/validation split
- threshold sweep process
- backtest rules
- paper-trading rules

The goal is a controlled comparison:

```text
PPO-only
vs.
PPO + Random Forest gate
vs.
PPO + XGBoost gate
```

---

## Model status

```text
Model: PPO + Random Forest hybrid
Stage: Validation baseline
Purpose: Backtesting, paper testing, and future XGBoost comparison
Production status: Not production-ready
```
