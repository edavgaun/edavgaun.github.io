---
layout: project
title: "The Core-Periphery Structure of Mexican AI Research Institutions"
award: "3rd place · MICAI 2026"
description: >-
  A 25-year longitudinal network analysis of institutional collaboration in the
  MICAI proceedings (2000–2025). The network grew sixteen-fold, but it did not
  become more integrated: a small core of six institutions carries most of the
  cross-cluster connectivity.
tags: [Network science, Scientometrics, Null models, LLM-assisted extraction]
kpis:
  - value: "53 → 852"
    label: institutions in the network, 2000 → 2025
  - value: "z = −11.32"
    label: giant component vs. 200 degree-preserving null networks (2025)
  - value: "234×"
    label: denser inside the 6-institution core than the network as a whole
links:
  - label: Read the paper
    url: https://doi.org/10.1007/978-3-032-44179-9_39
  - label: Interactive story
    url: /projects/micai-story.html
  - label: Live dashboard
    url: https://micai2026-mex-ia-evloution.streamlit.app/
  - label: Previous study (2025)
    url: /projects/micai-25-years/
authors: "Edgar Avalos-Gauna (Rice University) & Leon Palafox (Universidad Panamericana)"
venue: "MICAI 2026 · Springer LNAI 17150"
---

## Research question

> *Does a research ecosystem become more integrated just because it grows?*

The usual way to describe a scientific community is to count it: more papers, more institutions, more collaborations. Building on our [2025 study of MICAI's topics and reach]({{ '/projects/micai-25-years/' | relative_url }}), this paper treats the link between **growth** and **integration** as an empirical question and tests it against random expectation, using the complete record of the Mexican International Conference on Artificial Intelligence (MICAI), Mexico's main AI research forum since 2000.

## Data and pipeline

- **Corpus:** every MICAI proceedings volume from 2000 to 2025 (Springer LNAI/LNCS).
- **Extraction:** title, authors, affiliations and locations were extracted from scanned proceedings pages with `gemini-3.1-flash-lite` via the Gemini API.
- **Validation:** a stratified sample of 96 papers was independently re-annotated and cross-checked with Claude Sonnet 4.5 as an evaluation judge: **87.5% top-1** and **96.9% top-3** accuracy.
- **Normalization:** bilingual names, acronyms and campus variants were merged through a manually curated mapping table; countries were assigned from affiliation locations.
- **Network:** one cumulative, undirected graph per year. Nodes are institutions and edges are co-authored papers.

## Finding 1: growth is not integration

From 2000 to 2025 the network grew from **53 institutions and 45 links** to **852 institutions and 1,326 links**. Yet when each year's network is compared with 200 configuration-model networks that keep every institution's number of links but shuffle who connects to whom, the observed giant component is consistently **smaller than chance**, and the gap widens over time.

![Giant component and transitivity, observed vs. null model]({{ '/assets/img/micai/null-model.png' | relative_url }})

| Year | Observed GC | Null GC (mean) | z-score |
|---|---|---|---|
| 2010 | 61.02% | 71.73% | −6.00 |
| 2025 | 70.66% | 81.19% | **−11.32** |

A double-edge-swap randomization gives the same answer (z = −12.98). Transitivity explains why: at **0.121**, it is more than three times the null expectation (0.035). New collaborations mostly reinforce existing clusters instead of bridging separate ones.

## Finding 2: a small, dense core

![MICAI institutional collaboration network, 2025]({{ '/assets/img/micai/network-2025.jpg' | relative_url }})

Community detection finds **201 communities** (Q = 0.623); the largest holds only 15.4% of institutions. Just **6.7% of institutions account for 80%** of total betweenness centrality. The six most central are IPN, ITESM, CINVESTAV, INAOE, UNAM and TecNM, and they are tightly linked to each other: **13 of 15 possible edges** (density 0.867 vs. 0.0037 network-wide). Cross-cluster connectivity is routed through this core.

## Finding 3: four turning points

![International Collaboration Ratio over time]({{ '/assets/img/micai/icr.png' | relative_url }})

- **2008–09:** papers fell from 94 to 62 during the global financial crisis.
- **2010:** the International Collaboration Ratio peaked at 0.57 at MICAI's tenth-anniversary edition in Pachuca.
- **2023:** paper volume stayed typical (81), but new collaborations hit a record 105, coinciding with the rise of generative AI.
- **2024:** participation fell to 37 papers (from 141 submissions), the lowest since 2002.

The deep-learning boom (around 2012) and COVID-19 (2020) produced no comparable inflection.

## Policy implications

A core-periphery network is fragile: peripheral institutions reach each other through the core, so losing core capacity can fragment the ecosystem. Adding participants alone does not fix that. The paper suggests:

1. **Co-funding periphery-to-periphery projects**, not only periphery-to-core partnerships.
2. **Twinning and mentorship** programs in which core institutions connect peripheral ones instead of acting as their only hub.
3. **Structural indicators** (periphery-internal density, core dependency) alongside participation counts.

## Limitations

- **One venue.** MICAI is a partial lens; the 2023–24 decline may reflect researchers moving to other venues.
- **Name resolution.** Unmapped peripheral institutions are reduced to auto-generated acronyms, which can merge distinct institutions. The six core institutions were all mapped manually.
- **Cumulative networks.** Yearly metrics describe an accumulating structure; a 5-year moving window was used as a robustness check.
- **Sample-based validation.** Extraction was audited on a stratified sample, not on every record.

## Cite

```bibtex
@inproceedings{avalosgauna2026coreperiphery,
  title     = {The Core-Periphery Structure of Mexican AI Research Institutions, A Longitudinal Network Analysis},
  author    = {Avalos-Gauna, Edgar and Palafox, Leon},
  booktitle = {Advances in Soft Computing. MICAI 2026},
  editor    = {Ponce, Hiram and Ochoa-Ruiz, Gilberto and M{\'e}ndez-Gurrola, Iris Iddaly},
  series    = {Lecture Notes in Computer Science},
  volume    = {17150},
  pages     = {658--676},
  publisher = {Springer, Cham},
  year      = {2027},
  doi       = {10.1007/978-3-032-44179-9_39}
}
```
