---
title: "Forechecking Pressure Topology: A Continuous Geometry Framework for Retrieval Denial"
excerpt: "Award-winning spatial analytics framework from the Big Data Cup 2026, predicting defensive-zone turnovers using tracking data and lane-removal dynamics."
layout: single
toc: true
toc_sticky: true
tags:
  - Hockey Analytics
  - Spatial Data Science
  - Predictive Modeling
  - Python
---

## Overview
Traditional hockey analytics often describe forechecking systems using discrete labels (e.g., 1-2-2 or 2-1-2). However, actual execution quality is continuous, dynamic, and heavily dependent on timing. 

In this research—which **won the student category at the Big Data Cup 2026**—we introduce **Retrieval Denial Topology (RDT)**. Instead of relying on static proximity counts, RDT models retrieval denial as an ongoing dynamic of lane removal over time. 

* **Authors:** Ryan Dajani, Luke Blommesteyn, Eric Schilha, and Yashna Garg
* **Dataset:** 10 Big Data Cup 2026 public games (5v5), segmenting 2,086 defensive-zone retrieval episodes across 14,921 tracking frames.

---

## The Methodology: Continuous Spatial Pressure

At any given frame, the model identifies the puck carrier and calculates a continuous defender pressure score $P(x)$ at the carrier's location:

$$P(x) = \sum_{i} \exp\left(-\frac{||x-x_{i}||^{2}}{2\sigma_{i}^{2}}\right) \exp\left(-\frac{\text{ETA}_{i}(x)}{\tau}\right)$$

### Key Innovations of the Pressure Score:
1. **Physical Plausibility ($\text{ETA}_i$):** Uses a bounded-acceleration reachability approximation to determine how fast a defender can realistically close ground.
2. **Directional Commitment ($\sigma_i$):** The spread parameter is direction-dependent. A defender skating directly toward the carrier creates a tight, intense pressure footprint, while one moving away features a heavily penalized, weaker footprint. 

### Corridor Costs & The 3-Second Closure Rate
The framework integrates this pressure field along four canonical exit routes: **the middle lane, strong-side boards, weak-side boards, and behind the net**. 

The minimum cost across these options identifies the carrier's instantaneous *cheapest corridor*. We evaluate the forecheck's efficacy by measuring the **3-Second Closure Rate**: how much the cost of that cheapest lane rises from $t=0$ to $t=3\text{s}$.

---

## Key Findings & Predictive Power

### 1. Massive Predictive Lift over Baselines
We evaluated the topology framework against standard industry baselines to predict defensive-zone turnovers (the primary supervised endpoint). RDT demonstrated a massive performance leap:

| Model Baseline | Stratified Cross-Validated AUC |
| :--- | :--- |
| **Pressure + Role Logistic (RDT)** | **0.742** |
| Pressure Gradient Boosting | 0.742 |
| Nearest-Defender Baseline | 0.640 |
| Defender-Count Baseline | 0.619 |

* **The Takeaway:** Incorporating the continuous spatial tracking structure yields a **+0.102 absolute lift (~16% improvement)** over a simple nearest-defender model. Furthermore, factoring in the roles of the secondary layers ($F2$ and $F3$) added significant signal over pressure volume alone.

### 2. High-Pressure Monotonic Response
Denial rates (turnovers + forced dump-outs) scale smoothly with pressure. In the lowest pressure decile, the denial rate sits at **46.1%**, scaling up monotonically to **64.1%** in the highest pressure decile.

### 3. The "Tight Squeeze" Archetype
Using $k$-means clustering ($k=4$), we mapped out coach-native tactical profiles. The most successful profile, labeled **Tight Squeeze**, pairs high immediate carrier pressure with highly compressed, synchronized $F2$ and $F3$ support geometry. This profile suffocates exit options, converting into a **62.4% combined denial rate**.

---

## Operational Deployment & Coaching Workflow

This framework transitions seamlessly into a video-room clip review pipeline focused on three distinct questions:
1. Which corridor did the carrier identify as the cheapest option at the start of the retrieval?
2. Did the forechecking unit successfully close that specific lane within the decisive first three seconds?
3. Did the secondary layers ($F2$ and $F3$) arrive in sync to trap the carrier after first contact?

We also introduced the **Team Forecheck Pressure Index (TFPI)** to benchmark process quality across teams, moving front offices past raw outcome biases and anchoring evaluation directly to structural execution.
