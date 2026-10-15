# Supervisor review checklist

Source: `/home/javed/Downloads/comments_slides_v0.5.pdf` (37 pages).
Reviewer: Benedikt Hilmes. Page numbers refer to the reviewed PDF.
Actual PDF annotation contents were extracted and matched to highlighted text.
This replaces the earlier checklist inferred from screenshots.

Checked items have been verified in the current source. Unchecked items are
pending implementation or require clarification. Per the user's instruction,
missing numbers now have editable `TBD` placeholders; a checked placeholder item
means its location is implemented, not that its numerical value is finalized.
Quoted comments preserve
the reviewer's wording (including typos).

## Where to enter your numbers

- Search for `USER VALUES` near the top of `main.tex`: replace `\pendingvalue`
  in setup commands and `\werplaceholder` in the remaining result commands.
- Model sizes are in **millions of parameters**. Use `\wersingle{5.3}` for
  QAT-only scores and `\werresult{12.3}{0.10}` for device results (mean and
  standard deviation). Digital scores remain centered; device-result means
  use leading-digit padding. The `U` column type additionally pads standard
  deviations only in columns containing a value such as `10.90`.
- These result commands update both the main and appendix tables automatically.
- Search for `FFNN Transducer: Error Breakdown`: replace each `\pendingvalue`
  in its rows with S/I/D percentages. The caption identifies the evaluation
  configuration; edit it if your error reports use a different search/setup.

## General / title page (p. 1)
- [x] **G01:** “General: I like one line per bullet point, but this is kind of personal” — shortened setup/model bullets and split dense setup content. Long paper titles and narrow-column explanations still wrap where needed.
- [x] **G02:** “if possible count only pages until „Thank you“ slide” — talk counter ends at Thank You; references are unnumbered and backup slides numbered separately.
- [x] **G03:** “reduce citation to 1 author” — already implemented by `format.lab.names` in `i6bibstyle.bst` (first author + superscript plus).
- [x] **G04:** Highlight on “Prof” with no comment text — current source already uses `Priv.-Doz. Ralf Schlüter`.

## Related work (p. 3)
- [x] **R01:** “Monotonic Transducer paper instead of Graves 12” — already uses Tripathi et al. in related work.
- [x] **R02:** “I think calling the last bullet point „SynaptogenML“ would be fine” — final entry heading shortened.

## Hardware prerequisites (pp. 7–12)
- [x] **H01 (p. 7):** Wan citation: “drop” — already removed.
- [x] **H02 (p. 7):** Wouters citation: “drop” — already removed.
- [x] **H03 (p. 7):** Infineon citation: “drop” — already removed.
- [x] **H04 (p. 8):** “I dont think we need the citation here, this is rather for the crossbar layout” — title citation already removed; layout figure retains its source.
- [x] **H05 (p. 9):** Square resistor symbol: “remvoe” — already removed.
- [x] **H06 (p. 9):** Heading citation: “drop cite” — already removed.
- [x] **H07 (p. 10):** Set inequality: “V < V_s” — already corrected.
- [x] **H08 (p. 10):** Intermediate states: “for the measured devices in synaptogen” — programming-reliability claim now scoped to those devices.
- [x] **H09 (p. 10):** Heading citation: “drop cite” — already removed.
- [x] **H10 (p. 11):** Heading citation: “drop cite” — already removed.
- [x] **H11 (p. 12):** “maybe call crossbar layout (or so) / drop cite” — already renamed “Memristor Crossbar Layout”, without title citation.
- [x] **H12 (p. 12):** Conductance mismatch: “but its still better than just one line!” — explained the offset reduction from differential pairs and remaining mismatch; reduced spacing to keep text above the footer.

## Deployment diagram (p. 14)
- [x] **D01:** “(full model)” → “drop” — already removed.
- [x] **D02:** “should” → “can” — already changed.
- [x] **D03:** Encoder: “Conformer” — architecture specified in the block.
- [x] **D04:** Joiner: “FFNN?” — feed-forward joiner specified.
- [x] **D05:** External LM: “remove here and add bullet point” — block and arrows removed; optional LM integration described in a bullet.

## Experimental setup (p. 15)
- [x] **E01:** BPE merges/labels: “just keep one” — kept 184 labels, omitted merge count.
- [x] **E02:** Features: “downsampling?” — added temporal-downsampling placeholder `\encoderDownsampling` for the user to fill.
- [x] **E03:** Model types: “größe?” — added model-size placeholders `\ctcParameterMillions`, `\ffnnParameterMillions`, and `\lstmParameterMillions`; retained known encoder and FFNN-predictor dimensions.
- [x] **E04:** QAT comma: “linebreak” — quantization settings moved to their own bullet.
- [x] **E05:** Data: “number of epochs” — added `\baselineEpochs`, `\qatEpochs`, and `\finetuningEpochs` placeholders for the user to fill.
- [x] **E06:** Stages: “rename” — renamed “Training and evaluation”; distinguished baseline, QAT from scratch, and device simulation.

## Results (pp. 16–21)
- [x] **T01 (p. 16):** “I think we can join this in one table / Bits -> weight bits” — consolidated CTC baseline/QAT/simulation; renamed bit-width headers consistently.
- [x] **T02 (p. 18):** “Filler result” highlighted without comment text — full 4-bit memristor results filled from the aggregated report through shared commands; missing QAT-only scores remain editable `TBD` values.
- [x] **T03 (p. 19):** Checkpoint fine-tuning: “from where?” — full-precision checkpoint specified as the starting point.
- [x] **T04 (p. 21):** “This is FFNN transducer right? maybe move this up one page” — FFNN transducer identified in title; ILM results moved before full-context results.
- [ ] **T05 (p. 21, optional):** “maybe we can argue that this is also the case for ctc, even though we dont present it here” — only discuss CTC with supporting evidence; CTC has no transducer predictor ILM. **Needs clarification:** whether the intended analogy is external-LM reliance or CTC acoustic-prior compensation.

## Future work (pp. 23–24)
- [x] **F01 (p. 23):** Uppercase “A” highlighted without comment text — changed to “acoustic”.
- [x] **F02 (p. 23):** Error Analysis: “Small error table in the restuls” — added a results slide with editable S/I/D error-rate cells for baseline, QAT, and device simulation.
- [x] **F03 (p. 24):** Energy/RTF sentence: “drop RTF from here” — RTF removed from that sentence; retained as a metric in the following study objective.
- [x] **F04 (p. 24):** Blank penalties: “be more general” — now discusses emission-score penalties/biases generally, with blank as an example.

## Verification
- [x] **V01:** Rebuilt with `latexmk -pdf -outdir=build main.tex`; visually checked setup, 4-bit results, error breakdown, and appendix placeholder layouts; `git diff --check` passed. Existing font/metadata/obsolete-option warnings and a missing bibliography page range remain.
- [x] **V02:** PDF checks confirm 28 talk slides ending at Thank You (28/28), 3 reference pages, and 7 independently numbered backup slides.

## Additional data consistency follow-up
- [x] Replaced the inconsistent 4-bit encoder+predictor QAT 4-gram filler entry with `\ffnnFourBitPredictorQatLmWer` in both tables; user will supply the confirmed value.
- [x] Full 8-bit model 4-gram WER reconciled to report experiment 170: **18.8 ± 1.24** in main, combined appendix, and deep-dive tables.

## Aggregated report import

Source: `/home/javed/memristor_runs_aggregated_report.txt`.
Experiment IDs are the numeric prefixes before `__`. WER means are rounded
to one decimal and report standard deviations to two decimals, without
recomputing the reported variance.

| Slide configuration / search | Experiment ID(s) | Imported WER (%) |
| --- | --- | --- |
| FFNN full 4-bit / lex-free | 131 | 37.4 ± 1.33 |
| FFNN full 4-bit / tree, no LM | 132 | 29.6 ± 2.39 |
| FFNN full 4-bit / 4-gram, ILM 0.4, ELM 0.5 | 135 | 12.8 ± 0.72 |
| FFNN encoder-only 4-bit / lex-free, tree, 4-gram | 40, 41, 42 | 10.1 ± 0.04; 9.1 ± 0.12; 6.6 ± 0.07 |
| FFNN full 8-bit / 4-gram, ILM 0.4, ELM 0.5 | 170 | 18.8 ± 1.24 |
| FFNN 4-bit fine-tuning / tree, no LM | 93 | 11.2 ± 0.11 |
| Full-context encoder+predictor / cached lex-free, tree, 4-gram | 227, 228, 230 | 12.8 ± 0.65; 10.7 ± 0.84; 8.0 ± 0.28 |
| Full-context full model / lex-free, tree, no LM | 100, 101 | 29.5 ± 1.14; 39.5 ± 1.13 |
| Full-QAT FFNN, predictor not offloaded / 4-gram | 200 | 21.8 ± 4.84 |
| Full-QAT FFNN, only first joiner layer offloaded / 4-gram | 226 | 6.8 ± 0.05 |

- Full 4-bit FFNN and full-context encoder+predictor 4-gram values use the
  lowest mean WER among their matching reported LM-scale settings (135 and
  230); the scales are noted on the slides. Existing encoder-only 4-bit and
  fine-tuning configurations retain their prior selected scales (0.3/0.5).
- Used cached full-context predictor results consistently (227/228/230),
  rather than mixing lex-free uncached experiment 99 with cached tree runs.
- Excluded debug, blank-penalty, alternate ADC, and 125-epoch variants from
  existing standard-configuration rows.
- Removed outdated one-/two-run footnotes from updated tables: this report
  does not provide sample counts, so they cannot be confirmed.
- Setup values and S/I/D remain placeholders: the report contains aggregate
  WER and RTF, not downsampling, parameter counts, or error breakdowns.
  Epoch suffixes identify particular variants, not a single common schedule.
- QAT-only placeholder scores and full-context full-model 4-gram WER are
  absent. CTC rows have no bit-width identifier, so their mapping to the
  deck's separate 8-/4-bit rows needs confirmation before import.

## Progress log
- Extracted all 34 highlight annotations: 31 with comment text and 3 without.
- Verified previously implemented items against the source; remaining fixes follow progressively.
- Implemented the actionable text, diagram, table, ordering, and footer changes.
- Rendered changed slides and corrected crossbar text overflow discovered during visual inspection.
- First pass complete: 32 of 38 review checklist items are implemented or were already present. Six remain data-dependent or need clarification (E02, E03, E05, T02, T05, F02).
- Revised PDF: `slides_beamer/build/main.pdf` (37 pages).
- User requested fillable spots instead of providing missing experiment data: added named setup/result commands and an error-breakdown table with `TBD` cells. Optional CTC analogy (T05) still needs clarification; it is not a numerical placeholder.
- Placeholder pass verified: 37 of 38 review items are implemented/already present, including fillable locations for missing numbers. Current PDF has 38 pages (`slides_beamer/build/main.pdf`).
- Imported matched report results into main and appendix tables; retained unsupported placeholders. Build verification follows.
- Report import and alignment verified: build passed and shared 18.8 ± 1.24
  result appears in all three relevant tables. Replaced ad hoc padding with
  `\werresult`, `\wersingle`, and `\werplaceholder`, all using `\phantom`.
  Decimal points and ± positions in each numeric column on PDF pages 17, 18,
  19, 21, 23, 36, and 37 agree within 0.05 pt. Visually checked the ILM table
  as well and corrected the fine-tuning panel overflow. `git diff --check` passed.
- Following visual feedback, removed the fixed-width phantom fields: digital
  scores and TBD entries are centered under their headers again, and device
  results use ordinary spacing around ±. This supersedes the fixed decimal/
  ±-position alignment described in the previous entry.
- Final alignment correction: restored leading-digit `\phantom` padding only
  for device-result means, with standard-deviation padding scoped to the tree
  columns containing `10.90` (column type `U`). Digital/QAT scores and TBD
  entries remain naturally centered. Verified mean decimals, ± signs, and
  standard-deviation decimals within 0.05 pt on pages 18, 19, 21, 23, 36, 37;
  baseline scores on page 18 are centered under their headers within 0.01 pt.
  Build and visual checks passed, including the main and combined appendix table.
