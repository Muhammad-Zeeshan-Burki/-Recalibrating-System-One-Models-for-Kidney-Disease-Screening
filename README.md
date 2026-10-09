# Recalibrating System One Models for Kidney Disease Screening

**This repository accompanies a research paper.** It contains the code and the complete set of
outputs used to produce the experiments, figures and tables of the manuscript, and is published
solely so that the study can be reproduced and checked independently.

> It is research code, not a medical device. Nothing here is clinically validated and nothing in
> this repository should be used to make decisions about patient care.

## What is in this repository

| Path | Description |
| --- | --- |
| `CKD_System_One_Reliability_Study.ipynb` | The single notebook that runs the whole study end to end. |
| `outputs_laptop8gb/figures/` | IEEE-format figures (vector PDF + 600 dpi PNG) and `figure_captions.md`. |
| `outputs_laptop8gb/tables/` | LaTeX (`*.tex`) and CSV versions of every table, plus `hypothesis_verdicts.json`. |
| `outputs_laptop8gb/preds/` | Per-run prediction checkpoints (`.npz`), one file per arm x label budget x draw. |
| `outputs_laptop8gb/cache/` | Cached intermediate results (NHANES table, zero-shot scores, reliability suite). |
| `outputs_laptop8gb/logs/` | `manifest.json` (software/hardware/config fingerprint), `run.log`, `design_signature.txt`. |


## Reproducing the results

Two levels of reproduction are supported:

1. **Tables and figures from the shipped predictions (minutes, no GPU needed).**
   Keep `outputs_laptop8gb/` in place and re-run the notebook with `CKD_PROFILE=laptop8gb`.
   Every stage reads its checkpoint from `outputs_laptop8gb/` and recomputes only what is
   missing, so the analysis, figures and tables are regenerated from the archived runs.

2. **Full re-run from public data (hours, GPU required).**
   Delete or move `outputs_laptop8gb/` (and, if you want freshly downloaded data,
   `nhanes_raw/`) and run the notebook top to bottom. NHANES files are downloaded automatically
   from the CDC.

### Requirements

- Python 3.12 (other recent 3.x versions are expected to work)
- PyTorch with CUDA for the real profiles; CPU-only is enough for the `smoke` profile
- The notebook installs any missing Python packages itself (`numpy`, `pandas`, `scipy`,
  `scikit-learn`, `matplotlib`, `xgboost`, `pyarrow`, `tqdm`, `requests`, `statsmodels`,
  `transformers`, `peft`, `accelerate`, `tabpfn`, `laya`, ...)

### Profiles

Set `CKD_PROFILE` before starting Jupyter, or edit the `PROFILE` line in the first code cell:

| Profile | Purpose | Runtime |
| --- | --- | --- |
| `smoke` | Synthetic data and tiny random stand-in models; verifies the whole pipeline with no downloads and no GPU. Numbers are meaningless. | ~3-6 min |
| `quick` | Real NHANES and real models at heavily reduced sizes; verifies downloads, model loading and VRAM headroom. | ~30-60 min |
| `laptop8gb` | The full study as reported, sized for an 8 GB GPU. **Default; used for the paper.** | ~6-12 h |
| `colab_t4` | The full study sized for a free Colab T4. | ~12 h |

### Optional access tokens

Tokens are read from environment variables (or Colab secrets). Do not hard-code them in the
notebook.

- `TABPFN_TOKEN` - free TabPFN licence token from <https://ux.priorlabs.ai>. Required for the
  TabPFN arm; without it that arm is skipped and everything else still runs.
- `HF_TOKEN` - Hugging Face token, only needed if a model you load is gated.

### Determinism

The study seed is `20261002`. Label-budget draws are derived from the seed, the label budget `K`
and the draw index, so every arm receives exactly the same labelled subset for a given
`(K, draw)` pair. `outputs_laptop8gb/logs/manifest.json` records the seed, the full
configuration, package versions, GPU and the data-file checksums of the reported run, and
`design_signature.txt` guards against reusing cached runs after the data or splits change.

## Data

NHANES is public, de-identified survey data released by the CDC/NCHS. The notebook downloads the
required `.xpt` files on first use and caches them in `nhanes_raw/` (not tracked by git). No
individual-level data beyond these public files is included in this repository.

## Citation

If you use this code, please cite the accompanying paper.
