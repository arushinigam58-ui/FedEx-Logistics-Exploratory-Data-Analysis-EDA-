# 📦 FedEx Logistics — Supply Chain Exploratory Data Analysis (EDA)

Exploratory Data Analysis of a global health-commodity supply chain dataset (shipment modes, vendors, countries, freight cost, weight, and delivery timelines) to uncover cost drivers, delivery-delay patterns, and operational risks — with actionable recommendations for a logistics provider like FedEx.

## 📌 Project Overview

This project analyzes the **SCMS (Supply Chain Management System) Delivery History Dataset**, which records international shipments of health commodities (HIV test kits, ARVs, and related medical supplies) across 40+ countries. The goal is to answer concrete business questions about **delivery delays, shipment-mode efficiency, freight cost drivers, and INCO term performance**, then translate the findings into operational recommendations.

**Key business questions investigated:**
1. Do shipments from certain countries experience more delays than others?
2. Does shipment mode (Air, Ocean, Truck, Air Charter) impact on-time delivery?
3. Does the lead time between PO date and scheduled delivery date affect delay frequency?
4. Does the INCO term (EXW, FCA, RDC, DAP, etc.) affect vendor delivery performance?
5. Are higher-weight shipments more likely to incur higher insurance costs?

## 🗂️ Repository Structure

```
├── FedEx Logistics Supply Chain - EDA Project.ipynb   # Main analysis notebook
├── SCMS_Delivery_History_Dataset.csv                  # Raw dataset
└── README.md
```

## 📊 Dataset

**Source:** SCMS Delivery History Dataset (health-commodity supply chain shipments)

Key columns used in the analysis:

| Category | Columns |
|---|---|
| Shipment info | `Shipment Mode`, `Vendor INCO Term`, `Fulfill Via`, `Managed By` |
| Geography | `Country`, `Manufacturing Site` |
| Cost & weight | `Freight Cost (USD)`, `Weight (Kilograms)`, `Line Item Value`, `Line Item Insurance (USD)`, `Unit Price`, `Pack Price` |
| Dates | `PO Sent to Vendor Date`, `Scheduled Delivery Date`, `Delivered to Client Date` |
| Product | `Product Group`, `Dosage Form`, `Molecule/Test Type`, `Brand` |

## 🛠️ Tools & Libraries

- **Python** — Pandas, NumPy for data wrangling
- **Matplotlib**, **Seaborn** — static visualizations
- **Plotly Express** — interactive charts
- **Jupyter Notebook**

## 🧹 Data Cleaning & Feature Engineering

- Converted `Freight Cost (USD)` and `Weight (Kilograms)` from text/object columns to numeric, handling non-numeric entries (e.g. "Weight Captured Separately") and imputing with the median.
- Parsed `PO Sent to Vendor Date`, `Scheduled Delivery Date`, and `Delivered to Client Date` into proper datetime formats.
- Engineered two new features:
  - **`Days_To_Schedule`** — lead time between PO issue and scheduled delivery.
  - **`Is_Delayed`** — boolean flag comparing actual vs. scheduled delivery date.
- Imputed missing categorical values (`Shipment Mode`, `Dosage`, `Line Item Insurance`) using the mode.
- Verified zero remaining nulls and checked for duplicate records before analysis.

## 📈 Exploratory Analysis (20 Charts)

The notebook walks through 20 visualizations, each paired with a "Why," "Insights," and "Business Impact" note. Highlights:

- **Shipment Mode Distribution** — Air dominates (~6,400 shipments) vs. Truck (~2,800); Air Charter & Ocean combined are under 700.
- **Top Countries by Volume** — South Africa, Nigeria, and Côte d'Ivoire are the top 3 destinations, all PEPFAR-priority nations.
- **Freight Cost & Weight Distributions** — both are heavily right-skewed, with a small number of extreme high-cost/high-weight outliers.
- **Freight Cost vs. Weight** — a visible cost ceiling where shipments shift to cheaper modes above a weight threshold.
- **Correlation Heatmap** — Line Item Value, Quantity, and Insurance are strongly correlated (0.80–0.96); Freight Cost is essentially uncorrelated with everything — a sign of flat-rate pricing rather than value/weight-based pricing.
- **INCO Term Analysis** — vendor-controlled terms (CIF, DAP) show wider, higher freight cost distributions than buyer-controlled terms (EXW, FCA).
- **Weight vs. Insurance Cost** — insurance tracks *declared value*, not weight, confirming pricing should be value-based.

*(Full chart-by-chart breakdown with interpretations is in the notebook.)*

## ✅ Milestone Answers

| # | Question | Answer |
|---|---|---|
| 1 | Do certain countries see more delays? | Yes — countries with less-developed logistics infrastructure (e.g. Côte d'Ivoire, Nigeria) show more delays; South Africa performs best. |
| 2 | Does shipment mode affect on-time delivery? | Yes — Air is most reliable; Truck sees moderate delays from customs/infrastructure; Ocean has the longest and most variable lead times. |
| 3 | Does PO-to-delivery lead time affect delays? | Yes — compressed scheduling windows sharply increase delay frequency. |
| 4 | Does INCO term affect performance? | Yes — EXW shifts logistics risk to the buyer and is less predictable; RDC-routed shipments are pre-optimized and more reliable. |
| 5 | Do heavier shipments cost more to insure? | No — insurance cost correlates with declared value, not weight. |

## 💡 Recommendations

1. **Automated mode-switching** — rule-based logic to shift shipments from Air to Ocean/Truck once weight and timeline thresholds allow, cutting premium freight spend.
2. **Data-entry standardization** — enforce numeric-only validation on Freight Cost and Weight fields to eliminate corrupted values (e.g. "Weight Captured Separately").
3. **Strategic lead-time buffers** — mandate minimum PO-to-delivery windows on high-risk lanes (e.g. specific African destinations under EXW terms) to reduce rush-order delays.

## 🏁 Conclusion

The supply chain is heavily air-dependent and generally efficient, but the analysis surfaces clear, fixable vulnerabilities: inconsistent data entry, compressed vendor lead times, flat-rate freight pricing that ignores weight/value, and country-specific bottlenecks. Addressing these through data validation, INCO-term optimization, and value-based insurance pricing can reduce costs while improving on-time delivery performance.

## ▶️ How to Run

```bash
git clone https://github.com/arushinigam58-ui/FedEx-Logistics-Exploratory-Data-Analysis-EDA-.git
cd FedEx-Logistics-Exploratory-Data-Analysis-EDA-
pip install pandas numpy matplotlib seaborn plotly jupyter
jupyter notebook "FedEx Logistics Supply Chain - EDA Project.ipynb"
```

> Note: the notebook currently reads the dataset from a local Windows path (`C:\Users\admin\Downloads\...`). Update the `pd.read_csv(...)` path to `SCMS_Delivery_History_Dataset.csv` (relative path) before running.

## 👤 Author

**Arushi Nigam**
[LinkedIn](https://linkedin.com/in/arushi-nigam-b71075230) · arushinigam58@gmail.com-
