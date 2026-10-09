**Fig. 1.** Study design. Every arm receives the same K labelled participants (D random draws) and is evaluated on the same internal and temporally shifted test sets; the reliability suite probes clinical behaviour of the predicted probabilities.

**Fig. 2.** Label-budget curves on the internal test set (mean and 95% interval over random label draws). Markers at $K{=}0$ show zero-shot arms without adaptation. (a) AUROC, (b) Brier score, (c) calibration slope (ideal = 1, dashed).

**Fig. 3.** Reliability diagrams (equal-mass bins, averaged over label draws) at $K{=}64$ for the internal test set (a) and the two temporally shifted test sets (b), (c). The dashed line is perfect calibration.

**Fig. 4.** Clinical reliability suite at $K{=}256$. (a) Violations of clinically expected monotonicity (risk should not fall as age, systolic pressure, HbA1c, diabetes or hypertension increase). (b) Share of cases whose predicted risk changes by more than 0.10 under formatting or unit restatement (text arms only; tabular arms are invariant by construction). (c) Discrimination as input fields are removed. (d) Share of predictions that become extreme (<0.02 or >0.98) when an implausible value is injected.

**Fig. 5.** Mechanism ablation. (a) Brier score of the same System One backbone fine-tuned with different training objectives, after temperature scaling on a separate calibration set. (b) Paired difference to the log-score (cross-entropy) objective with 90% intervals; the grey band is the pre-registered equivalence margin ($\pm$0.005).

**Fig. 6.** Temporal shift at $K{=}64$. (a) Calibration-in-the-large across test periods (0 = average predicted risk matches observed prevalence). (b) Brier score on the 2021-2023 test set before and after recalibration with a small labelled sample from the target period.

**Fig. 7.** (a) Risk--coverage curves: error rate when only the most confident fraction of cases is decided automatically (threshold fixed on a validation split). (b) Decision-curve net benefit on the internal test set at $K{=}64$.

