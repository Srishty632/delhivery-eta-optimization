# delhivery-eta-optimization
Graph-based ETA prediction for Delhivery logistics-
# Optimizing Delivery ETAs with Graph-Based Network Intelligence
**Consulting & Analytics Club — IIT Guwahati | Summer Projects 2026**

---

## Problem
Delhivery's OSRM routing system underestimates actual delivery time 
on 94.6% of network corridors. This causes SLA breaches, failed 
customer promises, and broken capacity planning across the network.

---

## Approach
Built a complete graph-based intelligence system on real Delhivery 
logistics data (144,867 trips, 1,657 hubs, 2,783 corridors).

### Pipeline
1. **Data Exploration** — Confirmed OSRM underestimates actual time by 2.06x on average
2. **Data Cleaning** — Winsorization, outlier treatment, feature engineering
3. **Graph Construction** — Directed weighted graph (NetworkX); edge weights = median delay ratio
4. **Bottleneck Analysis** — Betweenness centrality + composite bottleneck score
5. **Baseline Model** — XGBoost ETA predictor (trip features only)
6. **Graph-Enhanced Model** — node2vec + GraphSAGE embeddings + ensemble
7. **FTL vs Carting Framework** — ML-backed route-type decision classifier

---

## Results

| Model | MAE | Within 15% | Notes |
|---|---|---|---|
| OSRM (current system) | 193.8 min | 3.71% | Delhivery's existing system |
| Baseline XGBoost | 28.3 min | 65.76% | Trip features only |
| Graph-Enhanced Model | 28.4 min | 72.77% | node2vec + GraphSAGE |
| FTL Framework | — | — | 99.88% accuracy, AUC 1.0 |

**Graph advantage: +7.01% within-15% over baseline (measured, not claimed)**
**MAE reduction: 165 minutes vs OSRM**

---

## Bottleneck Findings

Top 5 bottleneck hubs identified by composite score
(betweenness centrality + degree + delay + chronic rate):

| Rank | Hub ID | Connections | Avg Delay | SLA Contribution |
|---|---|---|---|---|
| #1 | IND000000ACB | 94 | 1.895x | 16.6% |
| #2 | IND562132AAA | 71 | 1.801x | 7.0% |
| #3 | IND501359AAE | 57 | 1.972x | 2.4% |
| #4 | IND712311AAA | 46 | 2.293x | 1.9% |
| #5 | IND160002AAC | 61 | 1.926x | 1.7% |

**Fixing top 3 hubs addresses 26% of all network SLA breaches.**

---

## Tech Stack
Python, NetworkX, PyTorch Geometric, node2vec, XGBoost,
GraphSAGE, Scikit-learn, Pandas, Matplotlib, Plotly

---

## Project Structure
