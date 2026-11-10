# Release checklist
- [ ] Run `pytest -q`
- [ ] Run `pairedrelperm --config configs/example.yaml`
- [ ] Inspect CSV/JSON/PNG outputs
- [ ] Confirm all example data are labeled synthetic
- [ ] Confirm no confidential or proprietary data are committed
- [ ] Confirm uncertainty inputs are standard uncertainties
- [ ] Predefine decision thresholds before real-data analysis
- [ ] Create a tagged GitHub release
