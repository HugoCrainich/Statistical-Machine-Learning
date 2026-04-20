# FedSpeak Analysis — NLP on FOMC Minutes

## Objective
Apply natural language processing and unsupervised machine learning to over two decades of Federal Open Market Committee (FOMC) meeting minutes, quantifying shifts in Federal Reserve communication tone, uncertainty signaling, and thematic composition across distinct monetary policy regimes.

---

## Methodology

**Text Preprocessing**
- Ingested raw FOMC meeting minutes spanning 20+ years of Federal Reserve deliberations
- Applied tokenization, lemmatization, and domain-aware stop word removal to normalize corpus vocabulary

**Feature Engineering**
- Constructed a TF-IDF document-term matrix incorporating unigrams and bigrams to capture both single-term frequency and co-occurrence patterns
- Applied PCA dimensionality reduction to TF-IDF vectors to denoise the feature space prior to clustering

**Sentiment Analysis**
- Scored each document using the Loughran-McDonald financial sentiment lexicon, a domain-specific dictionary calibrated for institutional and regulatory language
- Computed net sentiment (positive minus negative term frequency) and an uncertainty index per document

**Clustering & Regime Segmentation**
- Applied K-Means clustering to PCA-reduced TF-IDF vectors to identify latent thematic groupings across the corpus
- Conducted pre-COVID vs. post-COVID distributional comparison of sentiment scores to isolate pandemic-era communication shifts

---

## Key Findings

- **Cluster Structure:** [FILL IN — e.g., "Three distinct clusters emerged, broadly corresponding to easing, tightening, and crisis-response regimes, with post-2020 minutes disproportionately concentrated in the crisis cluster."]
- **Sentiment Trends:** [FILL IN — e.g., "Net sentiment declined sharply during the 2008–2009 and 2020 periods, with uncertainty scores reaching a 20-year high in Q2 2020."]
- **Pre- vs. Post-COVID Shift:** [FILL IN — e.g., "Post-COVID minutes exhibited a statistically significant increase in uncertainty language and a notable rise in bigrams associated with supply-side constraints."]

---

## Tools & Libraries
`Python` · `NLTK` · `scikit-learn` · `pandas` · `matplotlib` · `Loughran-McDonald Lexicon`
