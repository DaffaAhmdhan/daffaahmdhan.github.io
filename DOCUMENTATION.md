# Portfolio & Data Analytics Documentation

**Author:** Daffa Ahmadhan Khusumah  
**Primary Portfolio:** `portfolio/index.html`  
**GitHub Profile:** https://github.com/DaffaAhmdhan  

---

## 1. Overview & Redesign Changelog

This portfolio showcases 9 engineering, IT automation, IoT telemetry, research, and Data Analytics projects. It was redesigned from an Indonesian SaaS-style dark template into a clean, **English-first editorial engineering notebook** with:

1. **Humanized First-Person Copy:** Replaced third-person brochure phrasing, neon purple/pink gradients, and blur halos with direct engineering explanations, verified metrics, and concise prose.
2. **Synchronized Light / Dark Mode Toggle:** Defaults to a bright daylight palette (`#f8fafc` background, `#ffffff` cards, `#2563eb` accent) via `data-theme="light"` persisted in `localStorage.getItem('daffa_theme_v2')`, syncing theme state seamlessly between `portfolio/index.html` and all three standalone dashboards in `portfolio/dashboards/`.
3. **Interactive Case Studies for All 9 Projects:** Every project card features category filtering, live keyword search, verified KPI strips, and an expandable `<details>` engineering drawer containing architecture notes, SQL/Python/Batch/FSM snippets, and recommendations.
4. **Updated Repository Links:** Standardized GitHub links to `https://github.com/DaffaAhmdhan/...` matching the active GitHub account.

---

## 2. Directory Structure

```text
cv/
├── portfolio/
│   ├── index.html                           # Main English portfolio with Light/Dark toggle & 9 deep-dive case studies
│   ├── DOCUMENTATION.md                     # This architecture & reproduction guide
│   ├── CV_Daffa_Master_EN.pdf               # Downloadable English CV
│   ├── CV_Daffa_Master_ID.pdf               # Downloadable Indonesian CV
│   ├── photo.jpg                            # Profile photo
│   └── dashboards/
│       ├── telecom-sla-dashboard.html       # Synced Dashboard 1 (Chart.js + SQL drawer + Analyst Notes)
│       ├── ecommerce-rfm-dashboard.html     # Synced Dashboard 2 (Cohort Heatmap + RFM + Delivery Impact)
│       └── iot-telemetry-dashboard.html     # Synced Dashboard 3 (24h Diurnal Curve + Zone Anomaly Matrix)
└── projects/
    ├── telecom-it-sla-analytics/            # GitHub: DaffaAhmdhan/telecom-it-sla-analytics
    ├── ecommerce-cohort-rfm-analytics/      # GitHub: DaffaAhmdhan/ecommerce-cohort-rfm-analytics
    └── iot-telemetry-anomaly-analytics/     # GitHub: DaffaAhmdhan/iot-telemetry-anomaly-analytics
```

---

## 3. Data Analytics Pipelines (How It Works)

Each of the three new Data Analytics projects uses a reproducible local Python + SQLite pipeline with zero external package dependencies (standard library `csv`, `sqlite3`, `math`, `json`, `datetime`), ensuring every metric shown in the portfolio is backed by runnable code and SQL queries.

```text
[1] data/generate_data.py  ──>  [2] data/*.csv (raw records)
                                         │
                                         ▼
[3] src/run_analysis.py    ──>  Loads into SQLite DB + runs sql/*.sql
                                         │
                                         ▼
[4] output/*_metrics.json  ──>  [5] dashboard.html (Chart.js visualization)
```

### Project 1: Telecom & IT Service SLA Incident Analytics
- **GitHub:** https://github.com/DaffaAhmdhan/telecom-it-sla-analytics
- **Local Dashboard:** `portfolio/dashboards/telecom-sla-dashboard.html`
- **Dataset:** 5,000 synthetic IT/Telecom incident tickets (`Nov 2025 – Oct 2026`) across 5 regions (`Jakarta Selatan`, `Bogor`, `Bandung`, `Sukabumi`, `Depok`), 4 priority tiers (`P1`–`P4`), and 7 root causes.
- **SQL Techniques:** Star schema (`fact_tickets`), monthly CTEs with `LAG()` for MoM SLA delta, cumulative window sums for Pareto 80/20 breach ranking.
- **Verified Outputs (`output/kpi_summary.json`):**
  - Overall SLA Compliance: **79.3%** (3,965 / 5,000 within SLA)
  - Average MTTR: **16.41 hours** (P1 Critical: 2.60h; P2 High: 5.85h)
  - Repeat Incident Rate: **12.66%**
  - Regional Bottleneck: **Sukabumi** at **74.17% SLA** (18.49h MTTR) vs **Depok** at **81.68% SLA**
  - Pareto Concentration: Top 5 root causes generate **80.87%** of breaches (led by **Fiber Cut / ISP Upstream** at **23.0%** and **Power / UPS Fluctuation** at **18.36%**).

### Project 2: E-Commerce Cohort Retention & RFM Segmentation
- **GitHub:** https://github.com/DaffaAhmdhan/ecommerce-cohort-rfm-analytics
- **Local Dashboard:** `portfolio/dashboards/ecommerce-rfm-dashboard.html`
- **Dataset:** 2,400 customers and 6,581 orders (`Nov 2025 – Oct 2026`) totaling **Rp 4,182,594,000 (~Rp 4.18B)** GMV.
- **Analytical Techniques:** SQLite order/delivery aggregation + Python monthly cohort retention matrix (`M0`–`M5`) + quantile-based RFM scoring (`Champions`, `Loyal Customers`, `At Risk`, `Hibernating`, `Recent / Potential`).
- **Verified Outputs (`output/ecommerce_metrics.json`):**
  - **Champions** (12.0% of users, 289 customers) generate **30.7%** of revenue (Rp 1.28B, avg 5.48 orders, 37.8d recency).
  - **Champions + Loyal Customers** combined (59.7% of users) generate **79.2%** of revenue.
  - **At Risk** (274 customers, Rp 432.6M historical revenue) average **252.6 days** since their last order.
  - **Late Delivery Impact:** Delayed orders (1,156 orders, avg 8.02 days) drop average review scores from **4.25 to 2.45** and spike 1–2 star ratings from **6.38% to 55.1%**.

### Project 3: IoT Environmental & Energy Telemetry Anomaly Analytics
- **GitHub:** https://github.com/DaffaAhmdhan/iot-telemetry-anomaly-analytics
- **Local Dashboard:** `portfolio/dashboards/iot-telemetry-dashboard.html`
- **Dataset:** 17,280 hourly readings across 180 days and 4 facility zones (`Server Room A`, `Server Room B`, `RnEST Lab`, `Clinic / Lobby HVAC`).
- **Analytical Techniques:** Diurnal hourly SQL profiling, Peak (`09:00–17:00`) vs. Off-Peak power split, PLN commercial tariff modeling (Rp 1,444.70/kWh), and per-zone statistical Z-score anomaly detection (`|z| > 2.5`).
- **Verified Outputs (`output/iot_metrics.json`):**
  - Total Energy Footprint: **57,154.1 kWh** (est. **Rp 82.57M**), with Server Rooms A & B drawing **62.8%** (35,897.8 kWh).
  - Peak vs. Off-Peak Draw: Daytime average is **4.117 kW** (+45.9% over **2.822 kW** off-peak).
  - Anomalies & Breaches: **120 Z-score anomalies** and **102 thermal threshold breaches** (max 30.62°C in Room A, 31.32°C in Room B).
  - Optimization Potential: **Rp 4.62M** in 6-month savings from shifting 12% of peak cooling load via off-peak pre-chilling.

---

## 4. Catalog of Projects 4–9

| # | Project | Category | Links |
|---|---|---|---|
| **4** | Hospital Server Room Telemetry & Telegram Bot (`#TCK`) | IoT / Production Ops (RS Fatmawati) | [Live App](https://nextjs-app-ten-blue.vercel.app) &bull; [GitHub](https://github.com/DaffaAhmdhan/pemantauan-suhu-esp8266) |
| **5** | Automated Workstation Deployment Suite (`setup-komputer-baru.bat`) | IT Automation (RS Fatmawati) | Internal hospital unattended deployment suite |
| **6** | Online Retail Sales & Profitability BI Portfolio | Data Analytics / Web | [Live Demo](https://sales-analysis-portfolio.vercel.app) &bull; [GitHub](https://github.com/DaffaAhmdhan/sales-analysis-portfolio) |
| **7** | ACS Poverty & Demographic Data Explorer | Data Visualization / React | [Live Demo](https://acs-poverty-portfolio.vercel.app) &bull; [GitHub](https://github.com/DaffaAhmdhan/acs-poverty-portfolio) |
| **8** | Hybrid Spatial-Temporal Deep Learning for FMCW Radar HAR | AI & Signal Processing Research | [ARMADA Journal DOI](https://doi.org/10.55681/armada.v4i7.3001) |
| **9** | Contactless Body Temp IoT Scanner with Finite State Machine | Embedded Systems (SINTA 5) | [GitHub](https://github.com/DaffaAhmdhan/Sistem-Tertanam-) |

---

## 5. How to Run & Verify Locally

### Serve the Portfolio Website
Run a local static server from `d:\Project daffa\cv`:
```powershell
python -m http.server 8080 --directory portfolio
```
Open **http://localhost:8080** in any browser. Serving over HTTP ensures relative links to `dashboards/*.html`, `DOCUMENTATION.md`, and `CV_Daffa_Master_*.pdf` resolve cleanly.

### Re-Run All Data Pipelines
```powershell
python projects/telecom-it-sla-analytics/data/generate_data.py
python projects/telecom-it-sla-analytics/src/run_analysis.py

python projects/ecommerce-cohort-rfm-analytics/data/generate_data.py
python projects/ecommerce-cohort-rfm-analytics/src/run_analysis.py

python projects/iot-telemetry-anomaly-analytics/data/generate_data.py
python projects/iot-telemetry-anomaly-analytics/src/run_analysis.py
```
