# Predicting Yield

**Decoding Nitrogen Control of Yeast with Hybrid Mechanistic–ML Models**

Angel Bothra · Double major in Data Science and Biological Sciences, Krea University
Faculty Advisor: Dr. Vaishali Sharma · School of Interwoven Arts and Sciences (SIAS)

Presented at the **IIIT Sri City Research Expo 2026** (28 October 2026).

---

## The problem

In industrial fermentation, the same yeast strain run with the same process can give very different yields when only the **raw-material lot** changes. A lot is one supplier batch of a raw material such as yeast extract, peptone or molasses. Each lot carries a different amount and mix of nitrogen.

Yeast does not respond to nitrogen passively:

- It senses nitrogen outside the cell (SPS) and inside the cell (TORC1).
- It uses **nitrogen catabolite repression (NCR)** to use preferred sources first.
- It keeps **spare capacity in reserve**, buffering small changes.

So yield does not follow nitrogen in a straight line, and **no current model predicts a lot's yield from its nitrogen profile.**

## What the literature shows

This project began as an independent study (DATA 391) reviewing 20 papers, organised into five layers:

**Sense → Allocate → Quantify → Models → Predict**

| Model family | Strength | Limitation |
|---|---|---|
| Kinetic (Monod, mass balance) | Interpretable, little data; predicted an independent run with R² > 0.99 | One substrate; no NCR or reserves |
| Genome-scale (GEM, FBA, FVA) | Whole metabolic network; enzyme limits cut growth error 129% → 42% | Steady state; no nitrogen regulation; secreted protein overpredicted ~1,000× |
| Machine learning (ANN, LSTM, SVR) | Learns non-linear patterns; 47–86% lower error than classical growth curves | Black box; data-hungry; extrapolates poorly |
| **Hybrid (mechanistic + ML)** | ML learns the equations' residual error; test RMSE 5.60 → 2.87 on an unseen batch | Structure choice still an open question |

## Proposed approach

A hybrid framework that **combines existing models** rather than building from scratch, and fills the key gap: linking feedstock nitrogen to yield.

1. **Demand.** Nitrogen required by the target protein, from its amino-acid composition.
2. **Supply.** Each nitrogen form in a lot (YAN, forms, C:N) becomes an uptake limit, gated by an NCR switch.
3. **Cell model.** A genome-scale model with enzyme limits, a secretion and proteome layer, and NCR and reserve constraints.
4. **Learn.** ML corrects the mechanistic model's residual error; Monte Carlo sampling gives an uncertainty band.
5. **Output.** For each lot: predicted yield ± uncertainty, the limiting nitrogen source, and a resistance score based on FVA width.

**Hypothesis:** yield drops only when a lot's nitrogen pushes cells past their reserve capacity. Until then, NCR and reserves buffer the change.

Multi-omics (genomics, transcriptomics, proteomics, metabolomics) and structure prediction are planned to tailor the model to each host.

## Roadmap

- **Now:** review paper; public nitrogen datasets compiled
- **Phase 1:** build the demand, supply and cell layers in *S. cerevisiae*; test on simulated lots
- **Phase 2:** add ML correction and uncertainty; benchmark against kinetic-only and GEM-only models on held-out data
- **Phase 3:** validate with real raw-material lots; extend to a second host; explore a live digital twin

## Repository contents

| Path | What it is |
|---|---|
| [`docs/poster_A0.pdf`](docs/poster_A0.pdf) | Expo poster (A0) |
| [`docs/handout_A4.pdf`](docs/handout_A4.pdf) | Two-page project summary handout |
| [`references/REFERENCES.md`](references/REFERENCES.md) | The 20 reviewed papers |
| [`references/references_A4.pdf`](references/references_A4.pdf) | Printable reference sheet |

## Status

This is ongoing research. The review is complete; the model has not been built yet. Code and data will be added here as the framework is developed.

## Contact

Angel Bothra · angel_bothra.sias24@krea.ac.in · [LinkedIn](https://www.linkedin.com/in/angel-bothra-5a79ab277/)

---

© 2026 Angel Bothra. All rights reserved.
