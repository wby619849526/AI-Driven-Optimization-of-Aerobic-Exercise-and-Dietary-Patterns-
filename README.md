

## Code

| File | Purpose |
|---|---|
| `simulator.py` | CHRONO-SIM cohort generator and structural response model, BMHI, safety repair, reference plans |
| `gen_data.py` | Generates all raw data |
| `autograd.py` | Reverse-mode automatic differentiation on NumPy (gradient-checked) |
| `features.py` | Static features, hourly/daily tokens, chronotype-relative prescription encoding, similarity graph |
| `model.py` | CHRONO-RAGAT (circadian Transformer, RAGAT, chrono-nutritional cross-attention, FiLM, multi-task head) |
| `train.py` | Training with residual response propagation, inference, frozen-student surrogate |
| `optimizers.py` | CLO-GWO and baselines (GWO, mGWO, PSO, DE, GA, WOA, random search), batched |
| `exp_benchmark.py` | Experiment 1: 12 shifted benchmark functions, Wilcoxon/Friedman, CLO-GWO ablation |
| `exp_hpo.py` | Experiment 2: hyper-parameter optimisation (CLO-GWO vs random search) |
| `exp_predict.py` | Experiment 3: 5-fold CV, baselines, ablations, counterfactual ranking |
| `exp_prescribe.py` | Experiments 4–6: prescription optimisation, interpretability, in-silico RCT |
| `diagrams.py`, `make_figures.py` | Figures |
| `paper_*.py`, `write_paper.py`, `build_docx.js` | Manuscript assembly |

## Reproduce

Requirements: Python ≥ 3.10 with numpy, scipy, pandas, scikit-learn, matplotlib, pillow; Graphviz (`dot`);
Node.js with the `docx` package (manuscript only). No GPU is needed.

```bash
cd code
python gen_data.py                       # raw data
python exp_benchmark.py                  # Experiment 1
python exp_hpo.py CLO-GWO; python exp_hpo.py Random      # Experiment 2
python exp_predict.py tabular            # Experiment 3 (tabular baselines)
python exp_predict.py worker 0 1         # Experiment 3 (neural models; split across workers: worker i n)
python exp_prescribe.py                  # Experiments 4-6
python diagrams.py; python make_figures.py cohort benchmark hpo prediction ablation prescription personalisation trial interpret
python write_paper.py                    # manuscript
```

All random seeds are fixed; results are deterministic on the same library versions.
