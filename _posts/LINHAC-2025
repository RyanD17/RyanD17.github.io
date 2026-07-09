---
title: "Evaluating Goaltender Performance via Situational Expected Goals Sequence Modeling"
excerpt: "Research presented at LINHAC 2025 introducing a Markov Chain framework to isolate true goalie impact from structural team defense using tracking data."
layout: single
toc: true
toc_sticky: true
tags:
  - Hockey Analytics
  - Goaltender Evaluation
  - Markov Chains
  - Predictive Modeling
  - Python
---

## Overview
Evaluating goaltenders is one of the most notoriously difficult tasks in hockey analytics. Traditional metrics like raw save percentage are heavily influenced by the team's defensive structure, while standard Goals Saved Above Expected (GSAx) models often treat shots as isolated, independent events rather than the culmination of a sequence of plays.

Presented at **LINHAC 2025**, this research introduces the **Situational Expected Goals Differential (SEGD)** framework. By treating hockey as a continuous sequence of probabilistic events, we isolate a goaltender's true performance from the environment in front of them.

* **Authors:** Sean Chua, Luke Blommesteyn, and Ryan Dajani
* **Dataset:** Over 540,000 Sportlogiq tracking data events, modeling sequence-dependent game-state transitions.

---

## The Methodology: Markov Chain Sequence Modeling

Instead of analyzing a shot in a vacuum, our framework uses a **Markov Chain sequence-predicting model** to map out the exact sequence of play leading up to a shot (e.g., a turnover on a zone entry vs. sustained cycle pressure). This allows us to predict game-state probabilities dynamically as an attack develops.

### Quantifying the Crease High-Danger Zone
Our spatial danger heatmap mathematically isolates the high-danger zone directly in front of the crease, where shot conversion rates consistently peak at **25%–30%**. 

### Situational Expected Goals Differential (SEGD)
By comparing the cumulative probability of a sequence resulting in a goal against the goaltender's actual save performance, we calculate SEGD. 
* For low-danger chances, SEGD scales linearly with traditional Expected Goals ($xG$).
* For high-danger opportunities ($xG > 0.5$), the framework features increasing variance and steeper slopes—mathematically rewarding goaltenders who consistently make critical, high-pressure saves that swing games.

---

## Key Discoveries: Quantifying Score Effects

One of the most compelling findings of this framework is its ability to map out **Game State Performance Curves** and cleanly capture "score effects."

### The Hyper-Aggressive Delta
Our model shows that a goalie's SEGD peaks sharply at a **+6 score differential**. This perfectly models the reality of game dynamics: when a team is trailing heavily, they adopt hyper-aggressive, high-risk offensive tactics. This subjects the leading goaltender to a sudden influx of odd-man rushes and high-danger looks, which the SEGD framework accounts for and rewards.

---

## Operational Relevance for Front Offices & Scouters

For an NHL front office or a data firm like Stathletes, this framework serves two critical operational purposes:
1. **Lowers Onboarding Risk:** It proves the capability to handle, clean, and model highly complex micro-tracking event streams (540,000+ rows) rather than relying on public, flat event feeds.
2. **True Performance Isolation:** By adjusting for sequential context and score state, scouters can identify undervalued goaltenders playing behind porous defensive systems, or spot overperforming goalies insulated by elite defensive sequences.

[![GitHub Link](https://img.shields.io/badge/GitHub-View_Repository-blue?logo=github)](https://github.com/RyanD17/LINHAC-2025)

---
*For full methodology details, transition matrices, or code implementation specifics, please feel free to check out the repository or reach out directly.*
