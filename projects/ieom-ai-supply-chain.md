---
layout: project
title: "Tracing AI and Supply Chain Emphasis Across the Global IEOM Landscape"
award: "Best Track Paper · AI & Data Science · IEOM World Congress 2025"
description: >-
  The first comparative, NLP-based meta-analysis of IEOM proceedings: more than
  11,000 papers from seven regional conferences and the international edition
  (2017–2024), showing that AI and supply chain research is shaped by regional
  conditions rather than following a single global narrative.
tags: [NLP, BERTopic, Sentence embeddings, UMAP, TF-IDF, Streamlit]
kpis:
  - value: "11,000+"
    label: full-text IEOM papers scraped and analyzed, 2017–2024
  - value: "8 regions"
    label: seven regional conferences plus the international edition
  - value: "20 topics"
    label: from BERTopic on sentence-transformer embeddings
authors: "Edgar Avalos-Gauna (Rice University)"
venue: "2nd World Congress on IEOM · Windsor, Canada · October 2025"
---

## Research question

> *Do all regions talk about AI in supply chains the same way?*

AI-for-supply-chain research is usually reviewed as one global literature, drawn mostly from journals and from digitally mature economies. The IEOM Society runs conferences across Africa, Asia, Australia, Europe, India and the Americas, all with the same format, which makes its proceedings a rare dataset to compare how regions frame AI and supply chains, and how they reacted to disruptions such as COVID-19.

## Data and pipeline

- **Collection:** a Python scraper (requests + BeautifulSoup) traversed the IEOM digital library, extracting title, authors, abstract, keywords, conclusions, references, region, year and URL into JSON, with de-duplication by URL and title.
- **Quality filters:** papers without abstracts, shorter than three pages, or with malformed titles were removed. The Central America edition was excluded because of data inconsistencies.
- **Preprocessing:** lowercasing, NLTK stopwords plus domain terms ("ieom", "proceedings"), POS-aware lemmatization, and bigrams/trigrams.
- **Embeddings and topics:** sentence-transformer embeddings (≈11,297 × 384); PCA showed 90% of variance in 120 components, followed by UMAP and BERTopic with HDBSCAN (minimum cluster size 50).
- **Regional signatures:** normalized TF and TF-IDF by region and year, and a *Signature Score* (regional ÷ global TF-IDF) to find each region's distinctive vocabulary.
- **Exploration:** a custom Streamlit app for side-by-side comparisons across regions and editions.

![Paper count per IEOM region and conference maturity]({{ '/assets/img/ieom2025/papers-by-region.png' | relative_url }})

## Finding 1: a semantic map of IE/OM research

![UMAP projection of IEOM papers by thematic clusters]({{ '/assets/img/ieom2025/semantic-landscape.jpg' | relative_url }})

Each dot is a paper. BERTopic separates themes such as machine learning methods, supply chain and risk assessment, Industry 4.0, sustainability and green supply chains, lean six sigma, and inventory control and demand forecasting. Dashed lines mark the yearly centroid, showing how the community's focus moves over time.

## Finding 2: every region has its own fingerprint

![Most frequent and most distinctive topics by region and year]({{ '/assets/img/ieom2025/regional-topics.png' | relative_url }})

More than 60 curated terms were grouped into eight clusters (AI & ML, supply chain & logistics, Industry 4.0, data & analytics, optimization & modeling, human & management, sustainability & resilience, domain-specific). Tracking the most frequent and the most distinctive cluster per region and year shows:

- **Human & Management** dominates frequency almost everywhere, with sustainability taking over in several regions in 2023.
- **North America** moved from data & analytics to optimization & modeling, with Industry 4.0 as the most distinctive topic in 2024.
- **Europe** kept a sustained emphasis on optimization & modeling, shifting toward sustainability & resilience in 2023–24.
- **Africa** showed a jump to data & analytics and Industry 4.0 in 2023.
- **Australia** is the only region where supply chain & logistics emerged as the most distinctive theme (2024).
- Terms like **generative AI** and **LLM** appear asynchronously across regions, while **Six Sigma, TQM and lean** decline in both frequency and distinctiveness.

## Why it matters

Global AI and supply chain discourse is stratified by socioeconomic and institutional conditions. For IEOM, the framework can inform conference tracks and curricula; for researchers, it is a replicable method for conference-based meta-research and a way to spot emerging areas and potential collaborations.

## Limitations and next steps

- Regions and editions with inconsistent data were excluded, which limits representativeness.
- Topic labels were assigned manually; adding coherence and stability metrics would strengthen the trends.
- A mixed-methods follow-up with expert interpretation would help explain *why* topics emerge or fade in each region.

<p class="muted small">This paper received the Best Track Paper award (Artificial Intelligence and Data Science track) at the IEOM Society's Second World Congress on Industrial Engineering and Operations Management, Windsor, Ontario, October 14–16, 2025. It was presented at the congress but not included in the published proceedings.</p>
