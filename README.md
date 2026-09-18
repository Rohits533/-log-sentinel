# -log-sentinel
# Log Sentinel

Real-time anomaly detection for web server logs — using **semi-supervised learning** (trained on normal traffic only).

![status](https://img.shields.io/badge/status-active-brightgreen)
![python](https://img.shields.io/badge/python-3.11-blue)
![license](https://img.shields.io/badge/license-MIT-lightgrey)

## What it does

Log Sentinel ingests web server access logs, learns what "normal" traffic looks like, and flags anomalies in real time — attacks, error spikes, scraping bots, and unusual patterns — without needing labeled anomaly data.

It ships as a full-stack system:

- **Backend** — FastAPI service that ingests, parses, scores, and stores events
- **ML layer** — Semi-supervised anomaly detection (Isolation Forest baseline → Autoencoder)
- **Frontend** — Live dashboard showing traffic, scores, and flagged events
- **Deploy** — Backend on Render, frontend on Vercel

## Why semi-supervised?

In real production systems, **anomalies are rare and unlabeled**. You have plenty of normal traffic, but you almost never have a clean dataset of "this is what an attack looks like."

Semi-supervised / one-class methods solve this by learning only from normal data. They generalize to *unseen* anomaly types — critical for security, where new attack patterns appear constantly.

Research on industrial and network telemetry consistently shows autoencoders trained on normal data achieving F1 ≈ 0.94 and AUC-ROC ≈ 0.97, while maintaining balanced recall across both classes under extreme imbalance — where supervised and tree-based baselines collapse on the majority class.

## Architecture
