---
layout: project
title: "MICAI and the Making of AI in Mexico Through 25 Years of Data-Driven Insight"
award: "2nd place · MICAI 2025"
description: >-
  A computational analysis of 25 years of MICAI proceedings (2000–2024), Mexico's
  main AI conference. Bibliometrics and topic modeling trace how research shifted
  from logic and symbolic reasoning to data-centric machine learning and,
  most recently, LLMs.
tags: [NLP, Topic modeling (LDA), Bibliometrics, t-SNE]
kpis:
  - value: "25 years"
    label: of MICAI proceedings analyzed, 2000–2024
  - value: "10 topics"
    label: from LDA (coherence 0.42) on titles, abstracts, keywords and conclusions
  - value: "1,760"
    label: submissions mapped by country and institution
links:
  - label: Read the paper
    url: https://doi.org/10.1007/978-3-032-09044-7_5
  - label: Follow-up study (2026)
    url: /projects/micai-core-periphery/
authors: "Edgar Avalos-Gauna (Rice University), Leon Palafox & Lourdes Martínez-Villaseñor (Universidad Panamericana)"
venue: "MICAI 2025 · Springer LNAI 16222"
---

## Research question

> *How has AI research in Mexico changed over a quarter century, and what does its main conference reveal about where it is heading?*

MICAI has been held every year since 2000 and is the most influential academic AI forum in Mexico. This was the first full-scale computational study of its intellectual trajectory: what topics it covered, who contributed, and how the language of its papers changed.

## Data and pipeline

- **Corpus:** every MICAI proceedings volume from 2000 to 2024, downloaded from Springer's digital archive, plus scraped metadata (host city, date, volume size, publication type).
- **Cleaning:** a custom regex parser removed the repeated headers found in pre-2013 volumes; four comparable fields were kept per paper: title, abstract, keywords and conclusions.
- **NLP preprocessing:** lowercasing, NLTK and domain-specific stopwords, Gensim bigrams and trigrams, and WordNet lemmatization.
- **Models:** normalized keyword frequencies over time, LDA topic modeling, and t-SNE (after PCA to 150 components) to visualize semantic drift.

## Finding 1: a conference shaped by policy and events

![MICAI publication trends, 2000–2024]({{ '/assets/img/micai2025/timeline.png' | relative_url }})

Output grew quickly to a peak of over 120 papers in 2005. Several shifts followed: some submissions moved to IEEE proceedings in 2006; CONACyT's SNI criteria began favoring journals over conference papers in the late 2000s; COMIA launched in 2009 as a Spanish-language venue for students; the 2020 and 2021 editions were online; and from 2023 the conference put renewed emphasis on hands-on AI workshops.

## Finding 2: national core, international reach

![MICAI research output, domestic vs. international]({{ '/assets/img/micai2025/reach.png' | relative_url }})

Of 1,760 submissions, 793 came from Mexican institutions. ITESM led with 119, and central Mexico concentrates IPN, CINVESTAV, INAOE, UNAM and UP. Abroad, the largest contributors were Spain (61) and Brazil (55), followed by France (30), the United States (29), Colombia and China (27 each). Countries like Russia, Iran, Japan and India also appear, suggesting MICAI is an entry point for researchers outside the dominant publication circuits.

## Finding 3: from symbolic AI to data-centric AI

LDA identified ten topics, including supervised learning, reinforcement learning, robotics and computer vision, NLP, fuzzy logic, knowledge representation and evolutionary computation.

![Semantic drift of LDA topics, 2000–2024]({{ '/assets/img/micai2025/semantic-drift.jpg' | relative_url }})

Each panel follows one topic through the embedding space, from red (2000) to blue (2024):

- **Knowledge representation and fuzzy logic** cluster in the early 2000s, reflecting MICAI's symbolic and rule-based roots.
- **Reinforcement learning, learning strategies and robotics** persist across the whole period but drift toward newer paradigms.
- **NLP, clustering and optimization** are stronger in recent years.
- Papers from **2022–2024** converge toward the center of the map, consistent with a shift to data-centric AI. Terms such as *ethics* and *LLM* appear only in the most recent editions.

## Takeaways

- MICAI mirrors the global move from model-centric to data-centric AI.
- Mexican institutions remain the core of the conference, while its international reach spans Latin America, Europe and Asia.
- The paper proposes this framework as a reusable template for studying other national and regional AI communities, and points to collaboration networks as the next step, developed in the [2026 core-periphery study]({{ '/projects/micai-core-periphery/' | relative_url }}).

## Cite

```bibtex
@inproceedings{avalosgauna2025micai,
  title     = {MICAI and the Making of AI in Mexico Through 25 Years of Data-Driven Insight},
  author    = {Avalos-Gauna, Edgar and Palafox, Leon and Mart{\'i}nez-Villase{\~n}or, Lourdes},
  booktitle = {Advances in Soft Computing. MICAI 2025},
  editor    = {Mart{\'i}nez-Villase{\~n}or, Lourdes and V{\'a}zquez, Roberto A. and Ochoa-Ruiz, Gilberto},
  series    = {Lecture Notes in Computer Science},
  volume    = {16222},
  pages     = {57--72},
  publisher = {Springer, Cham},
  year      = {2026},
  doi       = {10.1007/978-3-032-09044-7_5}
}
```
