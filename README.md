# FS_SakshiKamble
Problem Statement- Student Commute Optimizer (Full Stack)
## 🏗️ System Architecture
# 🎓 Student Commute Optimizer — Full Stack Project

## 📌 Problem I’m Solving
Every day many students travel to campus alone. That wastes time, money, and fuel.  
This project helps students share rides safely and efficiently by matching students who travel similar routes — while keeping their home locations private and building trust within the community.

---

## 💡 What makes my solution different
I wanted to design a student-first, full-stack solution that focuses on **privacy, trust, adoption and sustainability**:

- **Pickup Zones (privacy-first)** — instead of showing exact home addresses, the system generates safe pickup zones (bus stops, cafes, gates) using DBSCAN clustering. Students meet at zones — not doorsteps.
- **Reputation Ledger (tamper-resistant)** — rides and feedback update a reputation stored in an append-only ledger (prevents manipulation).
- **Time-Elastic Matching** — flexible windows (e.g., ±10 min) let more matches succeed with little waiting.
- **Dynamic Ride Pools** — automatically merge overlapping pairs into 3–4 person pools when it saves time/fuel.
- **Sustainability + Rewards** — CO₂ saved is shown per ride, and students earn Commute Points redeemable for campus perks.
- **AI / Safety Layer** — lightweight anomaly detection flags suspicious patterns; an AI predictor pre-suggests common commutes.

---

## 🏗️ System Architecture (high-level)

```mermaid
flowchart TD
    subgraph Frontend [Student App (React + Mapbox)]
        F1[Anonymous Login]
        F2[Enter Route]
        F3[View Pickup Zones & Matches]
        F4[Chat & Rewards]
    end

    subgraph Backend [FastAPI / Node.js]
        A[API Gateway]
        M[Matching Engine]
        Z[Pickup Zone Generator (DBSCAN)]
        L[Reputation Ledger]
        S[Safety & Predictor]
        C[Chat Service (WebSocket)]
    end

    DB[(Postgres + PostGIS)]
    Redis[(Redis + H3 Index)]
    Routing[(OSRM / Mapbox Directions)]

    Frontend -->|REST / WS| A
    A --> M
    A --> Z
    A --> L
    A --> S
    A --> C
    M --> DB
    M --> Redis
    A --> Routing
