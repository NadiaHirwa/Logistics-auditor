# 🚚 The "Last Mile" Logistics Auditor
**Client:** Veridi Logistics (Global E-Commerce Aggregator)  
**Analyst:** Nadia Iradukunda Hirwa  
**Track:** Data Engineering — AmaliTech Apprenticeship Challenge  

---

## A. Executive Summary

Analysis of 96,470 delivered orders from the Olist Brazilian e-commerce dataset reveals that 6.77% of deliveries arrived late, with a direct and measurable impact on customer satisfaction. On-time deliveries average 4.29 stars while super-late deliveries collapse to 1.74 stars — a 2.55-point drop that proves logistics performance is the primary driver of negative reviews. The problem is not nationwide: it is concentrated in northeastern states, with Alagoas (AL) recording the highest late rate at 21.41% and São Paulo (SP) carrying the highest absolute volume of late orders at 1,820. A two-pronged intervention targeting AL (process fix) and SP (scale fix) would deliver the highest customer satisfaction improvement per dollar invested.

---

## B. Project Links

| Deliverable | Link |
|---|---|
| Notebook (Google Colab) | https://colab.research.google.com/drive/1cmZ6VKy09s_hesdEN_Q_v3RFWZdw8pwB?usp=sharing |
| Dashboard (Looker Studio) | https://datastudio.google.com/reporting/e6cc3feb-c04e-4cd3-83dd-76e13734d7a5 |
| 📑 Presentation | https://docs.google.com/presentation/d/e/2PACX-1vTOsNeYUek8slwxN6osWNpo-Avt6mJjVJbJ6qTOfgCxnpEedyVK54q7DAGnIU9ovPlqR1j0qeli6nsa/pub?start=false&loop=false&delayms=5000 |

---

## C. Technical Explanation

### Data Cleaning
- Loaded 4 relational CSV files: Orders, Reviews, Customers, and Products
- Filtered to **delivered orders only** (96,478 out of 99,441), excluding canceled and unavailable orders
- Deduplicated reviews by keeping the most recent review per order (resolved 529 duplicate order_ids caused by multiple reviews per order)
- Dropped 8 rows with missing delivery dates where delay could not be calculated
- Final clean dataset: **96,470 orders** across 13 columns

### Delay Calculation
- `days_difference` = `order_delivered_customer_date` − `order_estimated_delivery_date`
- Positive = late, Negative = delivered early
- Classification: **On Time** (≤ 0 days), **Late** (1–5 days), **Super Late** (> 5 days)

### Candidate's Choice — Business Risk Score
I added a **Risk Score** combining late delivery rate with order volume per state using the formula:  
`Risk Score = late_pct × log(1 + total_orders)`  

**Why:** A state with a 20% late rate but only 50 orders is less critical than a state with 12% late rate and 12,000 orders. The risk score surfaces states where fixing the problem will have maximum customer impact. This gives the CEO a prioritized action list — not just a ranked list of bad rates.

This analysis revealed that while **AL** has the worst late rate (21.41%), **SP and RJ** represent the highest business risk due to their combination of high volume and elevated late rates.

---

## D. User Stories Completed

| Story | Title | Status |
|---|---|---|
| Story 1 | The Schema Builder | ✅ Complete |
| Story 2 | The "Real" Delay Calculator | ✅ Complete |
| Story 3 | The Geographic Heatmap | ✅ Complete |
| Story 4 | The Sentiment Correlation | ✅ Complete |
| Bonus | The "Translation" Challenge | ✅ Complete |
| Extra | Candidate's Choice — Risk Score Analysis | ✅ Complete |

---

## E. Key Findings

- **6.77%** of delivered orders arrived late
- **AL** has the worst late rate: **21.41%**
- **SP** has the most customers affected: **1,820 late orders**
- On Time → **4.29 ⭐** | Late → **2.99 ⭐** | Super Late → **1.74 ⭐**
- Remote northern states (AM, RO, AP) surprisingly have **low** late rates
- The delivery problem is **regional, not national**

---

## F. Tech Stack

- **Python** — Pandas, NumPy, Plotly, Seaborn, Matplotlib
- **Google Colab** — Cloud notebook environment
- **Google Looker Studio** — Public interactive dashboard
- **Dataset** — [Olist Brazilian E-Commerce Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) via Kaggle

---

*This project was completed as part of the AmaliTech DEG Apprenticeship Programme — Data Engineering Track (July 2026 Intake).*