# LinkWeave: Link Prediction Model for Scale-Free Networks

An ensemble-style link prediction classifier for scale-free social networks, built in Python and trained on a large (40M+ interactions) real-world Twitter interaction graph dataset. The model uses an engineered feature set derived from network topology and directional network structure to predict whether a link exists between two nodes.

This project ranked in the top 1% of models in UPenn Network Theory and achieved an F1 score of 0.9810 when evaluated on a held-out network-link test dataset (n = 1.06M)

## Overview

The goal of this project is to predict missing or future edges in a sparse, scale-free, directed social graph. The approach here is deliberately structural: engineer informative graph features, build a strong supervised classifier, and evaluate it on balanced positive/negative link samples.

## Tech/Design Notes

- I designed the model's engineered features/extraction signals around the structure of scale-free directed networks, which have degree distributions that follow a [power law](https://aaronclauset.github.io/powerlaws/); this makes network sparsity and degree imbalance particularly relevant
- The engineered feature set spans several graph characteristics including: *direction-aware neighborhood overlap*, *cosine similarity*, *centrality*, and *path-based signals*
- Packages use: scikit-learn, NetworkX, pandas, and NumPy

## Feature Engineering

The core of the project is the feature construction. Instead of treating link prediction as a black box, the model explicitly captures multiple structural signals that often indicate latent connectivity in directed networks.

Engineered features include:

- **Common-following / common-followed-by counts**
- **Jaccard Similarity** on both inbound and outbound neighborhoods
- **Cosine Similarity** over directional neighbor sets
- **Adamic–Adar Index/Variants** for both predecessor and successor structure
- **Shortest-Path Signal** between node pairs
- **Preferential Attachment Ratio**

A key part of the project was extending standard undirected link-prediction heuristics into a directed-graph setting so the model could separately reason about who two nodes follow, who follows them, and how they sit in the broader network.

## Results

The model was evaluated on a held-out test dataset of Twitter network-link interactions. It achieved:
- **Top 1% model performance** in UPenn Network Theory
- **0.9810 F1 score** on the test dataset
- **0.9803 Macro-averaged F1 score** on the test dataset
- **98.35% link-prediction accuracy** on the test dataset
