# New-results slides: sources and scope

`new_results_slides.tex` expands the two original “New Stuff” draft frames. The blank-preference and clipping frames are merged; the former appendix “Full QAT FFNN Transducer Deep Dive” is consolidated with the ADC-precision frame in the main results sequence. Other original frames are retained. WER is on LibriSpeech dev-other. New tables round means to one decimal and standard deviations to two, following the deck. Single-run results have no uncertainty marker. Curves connect reported sweep points, not fitted estimates.

## Local sources

### Presentation review updates

- Fine-tuning comparison now includes QAT references: experiment 3 / F row 28 (FP32 to 8-bit: 6.5, 6.2, 4.9) and experiment 9 / F row 35 (8-bit to 4-bit: 7.5, 7.0, 5.4). Experiment 9A / row 36 changes inference ADC settings on that fine-tuned model; its memristor-simulated scores remain provisional (two runs). No new ADC 4/4 result is inferred.
- Single-run table values display plus/minus 0.00 with an asterisk, at the user's request. This is a single-run display convention, not a measured multi-run SD. Two-run scores retain their measured SD and an asterisk.
- Review wording for correction tolerance: “10% acceptable relative degradation” (numeric setting remains 0.10).

The slides are now incorporated directly into `main.tex`; the former `new_results_slides.tex` file has been removed. `figures/joiner_output_distributions.png` is a presentation copy of the original histogram with legends standardized to “QAT” and “Memristor simulated”; plotted data are unchanged. The caption retains the ADC 4/4 setting.

All sheet row references below are the visible spreadsheet row numbers, not HTML line numbers.

- `Master Results Sheet/FFNN RNN-T 2710.html` (F): experimental results.
- `Master Results Sheet/Weights Analysis QAT FFNN 0311.html` (W): weight distributions.
- `Master Results Sheet/Blank Bias Magnitudes.html`: embedded bias-statistics images; the W8A8 image is `resources/image_543442417_0.jpg`.
- Joiner distribution image: `Master Results Sheet/resources/image_760334962_0.jpg`, as embedded in F. It excludes blank and special tokens; it is not a blank-posterior heatmap or a direct per-ADC clipping-rate measurement.

## Slide mapping

1. **Excess blank preference**: existing main-deck 8-bit error breakdown; W8A8 bias-statistics image. Blank +1.39247, largest nonblank positive +0.39622. Heatmap placeholders removed at the user's request. The issue slide now combines the clipping mechanism, output distributions, bias/error statistics, and layer ablation.
2. **ADC clipping meets digital bias**: distribution image above; 28/10 notes link the unclipped digital bias and clipped weight contribution. Diagram is conceptual. Bias is added after the analog VMM/ADC; ordinary-token marginal histograms alone do not prove blank preference.
3. **ADC range**: F rows 12, 56, 58–61 (experiments 10, 10.B1, 10.B3–B6). Combined with the output-precision sweeps on the fixes slide, “ADC Tuning: Preserve Range, Reduce Precision”. The 8/8 vs. 4/8 comparison also changes precision, not range alone. Retain the positional-encoding exception. The reported comparison demonstrates sensitivity to the trained quantization grid as well as range; do not claim more precision must improve recognition.
4. **Layer choice and ADC budget (merged deep dive / precision)**: layer-ablation table transferred unchanged from the former appendix. ADC data: F rows 66–67, 71–73 (10.B11, B12, B16–B18); corrected 4-bit rows 86, 88–89 (11.B9, B11, B12). The 4-bit reference is the working, corrected model, per the user's clarification. These data test lower precision at the output, not all possible layer/ADC combinations. The merged slide uses current-sheet values: 8-bit output 2/6 is 13.24 ± 0.59 and 4/8 is 12.2. The removed appendix used an earlier sweep (aggregate report IDs 171, 173, 193, 172, 194): 2/6 was 12.3 ± 0.25 and 4/8 was 12.1; other displayed rounded values agree. Those earlier values are preserved here for provenance, not combined with the newer sweep. The sheet's D-series output-only sweep also uses that earlier 12.31 baseline; it is not used in the new joiner-2/6 charts.
5. **No output bias**: F rows 12, 15, 74, 76; experiment 10 digital/simulated vs. 13 digital and 13.B1/B3 simulated. Newly trained model, not post-hoc removal of a trained bias. Digital results are comparable, not identically equal. No-bias simulations are single runs.
6. **Digital vs. ADC-tuned penalties**: F rows 160, 164–170 (10.G1, G5–G11) and 122–123, 125, 128, 130–132 (10.D11–D21). The D11 onward block explicitly changes to **both joiner layers** at 2/6, unlike D1–D10 (output-only). Chart uses the main experimental cells, not inconsistent side-chart values. Baselines are aggregate means; other plotted points generally are single reported sweep scores.
7. **Pre/post penalty**: F rows 122, 125, 128, 130–138 (D11, D14, D17, D19–D27); 28/10 notes. A pre-softmax logit subtraction and a post-softmax log-score subtraction differ by state-dependent normalization. They are not mathematically identical despite similar best WER. No pre-softmax 4-gram sweep is supplied.
8. **ADC 4/4 penalty alone**: F rows 12 and 98–105 (10.C1–C8). Use main result columns (18.34 ± 0.49 at 2.5), not the conflicting side-chart value 18.84. Tree above 60% omitted from chart; values shown are actual evaluated points, not clipped points. Best reported greedy 18.34 and tree 20.06; not a single shared optimal penalty.
9. **Sparsity and steps**: W rows 3–4, 13–14; more precise steps in 20/10 call notes. Sparsity is a vulnerability hypothesis, not independently proven causality. Digital 4-bit score from F row 13.
10. **Joiner programming**: F rows 13, 83–87 (11, 11.B6–B10). Ideal programming and bounded correction are distinct. No blanket claim that joiner-only correction eliminates all full-model error. Correction parameters are transcribed as reported; “0.10 deviation” has no additional inferred unit.
11. **Full-model correction**: F rows 12–13, 68, 70, 90 (10, 11, 10.B13/B15, 11.B13). Default and corrected 8-bit cases use the same joiner ADC 2/6. Note source 4-bit LM standard deviation is 0.71, whereas the unchanged old deck uses 0.72.
12. **4-bit penalty**: F rows 150–156 (11.F1–F7). This sweep is **joiner corrected**, not uncorrected or full-model corrected. Tree baseline is an aggregate, remaining sweep entries are single scores. No 4-gram sweep supplied.
13. **Fine-tuning**: F rows 12–13, 28, 36, 68 (10, 11, 3, 9A, 10.B13). 4-bit fine-tuned values explicitly have two cycles. Deployment ADC configurations differ for scratch/fine-tuned 4-bit models: this is a practical comparison, not isolation of training method alone. 28/10 notes supply interpretation. Fine-tuning retains clipping sensitivity; lower programming sensitivity does not mean zero device degradation.
14. **Outliers/grid**: W rows 14–15, and rows 4–5 for the first-layer qualification. The output step improves 0.200 → 0.078; first-layer step instead increases 0.200 → 0.354. Regularization and observer reset are proposed experiments, not demonstrated solutions.

## Weekly call notes consulted

- [15/09](https://www.notion.so/3e3b55ed253680e4b206c7631dbe11cb), [22/09](https://www.notion.so/3e3b55ed25368022a160c2737e82662c): original deployment analysis.
- [29/09](https://www.notion.so/3eab55ed253680de8e0af14c5c89a251), [06/10](https://www.notion.so/3f1b55ed253680458f0afc2be5884f40), [13/10](https://www.notion.so/3f7b55ed25368016b32de366ecccd1f3): ADC and penalty experiments. Earlier penalty estimates were superseded; do not use 7.3 as an optimum or assert the earlier claimed exponential pre/post equivalence.
- [20/10](https://www.notion.so/3feb55ed25368081a201dcf73b0d1b27): sparsity, programming correction, quantization steps, corrected 4-bit penalty sweep.
- [28/10](https://www.notion.so/405b55ed253680feaefae1240c292d0a): no-bias training, pre/post penalty comparison, fine-tuning interpretation.
- [03/11](https://www.notion.so/409b55ed2536808ba15af73e8229e42c): full correction, output outliers, regularization/reset proposals.
- [10/11](https://www.notion.so/413b55ed2536804d8ae6d2471a80d6be): no-bias weight analysis and later adapter work. Adapter results excluded because they are outside the two draft frames.

## Preserved-content caveat

The original draft and future-work frames remain verbatim, as requested, so they may repeat the new findings or still describe completed experiments as future work. Updating/removing those frames is a separate editorial decision.
