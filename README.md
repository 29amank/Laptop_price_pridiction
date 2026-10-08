# Laptop Price Prediction — Streamlit Demo

A Python/Streamlit demonstration that predicts a laptop price estimate from user-selected hardware and product features.

> **Status:** Portfolio/learning project. The saved model artifacts and the current dependency versions have **not** been independently verified to load or produce accurate predictions. Do not treat outputs as current market prices or purchase advice.

## How it works

1. Select brand, laptop type, RAM, CPU, GPU, operating system, screen resolution, storage, and display features.
2. Enter laptop weight and screen size.
3. The app derives pixels per inch (PPI) from the chosen resolution and screen size.
4. A previously trained serialized machine-learning pipeline generates a prediction displayed on screen.

**Main entrypoint:** `app.py`  
**Bundled model files:** `pipe.pkl`, `df.pkl`  
**Training/analysis notebook:** `laptop-price-predictor.ipynb`  
**Dataset:** `laptop_data.csv` (check provenance and sharing rights before reusing it).

## Local setup

Install Python 3 and create an isolated environment:

```bash
git clone https://github.com/29amank/Laptop_price_pridiction.git
cd Laptop_price_pridiction
python -m venv .venv
```

Activate the environment:

- **Windows PowerShell:** `.venv\Scripts\Activate.ps1`
- **Linux/macOS:** `source .venv/bin/activate`

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

**Dependency-only verification:** On 2026-10-08, [GitHub Actions](https://github.com/29amank/Laptop_price_pridiction/actions/runs/37817547179) installed the listed packages, imported Streamlit/NumPy/pandas/scikit-learn, and compiled `app.py`. It deliberately **did not** load either pickle model or run prediction, so model compatibility and accuracy remain unverified.

Start the application:

```bash
python -m streamlit run app.py
```

The project expects the pickled model files in the same working directory as `app.py`. Specific versions of pandas, NumPy, scikit-learn and Streamlit originally used to produce the model were not recorded; compatibility may require finding and pinning those versions or retraining the model.

## Security and accuracy notes

- **Never unpickle untrusted files.** Python `pickle.load` can execute code while loading objects; inspect origin and trust of `pipe.pkl` and `df.pkl` before running the application.
- This app is a demo rather than a validated forecasting model. No accuracy metrics, evaluation dates, or benchmark results are claimed here.
- Enter a positive screen size; the existing implementation divides by screen size to compute PPI and does not yet validate a zero value.
- Check prediction units/currency and preprocessing consistency against the original training notebook before presenting predictions as meaningful figures.
- Existing `.pkl` and data files are already tracked; the new `.gitignore` does not change or validate them.

## Repository files

| File | Purpose |
| --- | --- |
| `app.py` | Streamlit user interface and inference |
| `pipe.pkl` | Serialized prediction pipeline |
| `df.pkl` | Serialized DataFrame for select-box options |
| `laptop-price-predictor.ipynb` | Model training/analysis notebook |
| `laptop_data.csv` | Included laptop data |
| `requirements.txt` | Approximate runtime dependencies; versions not pinned |
| `Procfile` and `setup.sh` | Legacy deployment configuration; not verified on modern hosting |

## Planned improvements

- Document training dataset license/provenance and model evaluation results.
- Reproduce model build with exact dependency versions.
- Add input validation for screen size and weight.
- Add a small inference smoke test and verify the prediction units.
- Review legacy hosting configuration before deploying.

## License and ownership

No `LICENSE` file is present in this repository. Reuse and redistribution terms have not been established. Check the licensing of the source, dataset, notebook, and serialized artifacts before redistribution.
