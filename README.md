# PairedRelPerm

A reproducible Python workflow for testing whether a before/after relative-permeability change is distinguishable from quantified uncertainty.

## What it does

- validates interpreted `Sw, kro, krw` data and standard uncertainties;
- fits constrained **Corey** or **LET** curves;
- runs paired Monte Carlo refitting;
- represents shared and run-specific error components explicitly;
- calculates realization-wise `delta kr = kr_after - kr_before`;
- reports percentile intervals and probabilities in the predefined desired direction;
- propagates fitted curves to fractional flow;
- writes CSV, JSON, and PNG outputs;
- includes synthetic data, tests, and GitHub Actions CI.

## Scientific scope

This release starts from **interpreted relative-permeability points**. It is not a validated inverse solver for raw pressure, rate, produced-volume, capillary-end-effect, or CT data. Results are conditional on the uncertainty model. A visible curve separation is not itself proof of treatment effect.

## Quick start

```bash
python -m venv .venv
# Linux/macOS
source .venv/bin/activate
# Windows PowerShell
# .venv\Scripts\Activate.ps1
pip install -e ".[dev]"
pytest -q
pairedrelperm --config configs/example.yaml
```

Outputs are created in `outputs/`.

## Input schema

| Column | Meaning |
|---|---|
| `Sw` | water saturation, fraction |
| `Sw_std` | 1-standard-uncertainty of water saturation |
| `kro`, `krw` | interpreted relative permeability |
| `kro_std`, `krw_std` | 1-standard-uncertainties of relative permeability |

## Decision principle

For realization `i`:

```text
delta_kr_i(Sw) = kr_after_i(Sw) - kr_before_i(Sw)
```

The package evaluates the distribution of this paired difference. Probability thresholds, practical-effect thresholds, desired direction, and the relevant saturation interval must be declared before reviewing results. They are project criteria, not universal SPE/SCAL standards.

See `docs/METHODOLOGY.md`, `docs/UNCERTAINTY_GUIDE.md`, and `docs/GITHUB_UPLOAD.md`.
