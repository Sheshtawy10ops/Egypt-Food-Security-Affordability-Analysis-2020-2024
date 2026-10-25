# Egypt Food Security & Economic Affordability Analysis (2020–2024)
**A Data-Driven Policy Intelligence Report | Digital Egypt Pioneers Initiative (DEPI) Capstone Project**

---

## 📌 Project Overview
* **Objective:** Quantify the compounded impact of Egypt's currency devaluation and food price inflation on household food affordability from 2020 to 2024.
* **Problem Statement:** Egypt experienced a **59.84%** peak EGP devaluation and a **63.57%** food inflation rate, creating a compounded affordability crisis for minimum-wage households.
* **Scope:** Analyzes 5 years of macroeconomic, agricultural, and international trade data (World Bank, WFP, FAOSTAT, UN Comtrade) across key food commodities and minimum-wage household affordability.
* **Outcome:** A 4-page interactive Power BI dashboard enabling policymakers to monitor affordability, price volatility, and import-concentration risk.

---

## 🎯 Target Audience
* **Ministry of Supply & Internal Trade:** Monitor commodity affordability and optimize subsidy targeting.
* **Central Bank of Egypt:** Understand FX devaluation impact on food import costs.
* **Ministry of Agriculture:** Identify local production gaps versus import dependency.
* **Policy Advisors & Economic Researchers:** Access data-backed evidence for economic reform scenarios.

---

## 🛠️ Tools & Technologies
* **Power BI Desktop:** Data modeling, DAX measures, and final interactive dashboard design (utilizing custom visuals including `Datepicker`, `Timeline`, and `Tachometer`).
* **Power Query (M Language):** ETL pipeline and data transformation.
* **Figma:** Wireframing and dashboard layout design.
* **Gemini:** Data extraction and insight generation.

---

## 📊 Data Sources & Data Model

### Data Sources:
* **World Bank WDI:** Income per capita, Headline CPI, and official exchange rates.
* **CAPMAS & HDX (WFP):** Local Egyptian food commodity prices (`WFP_FOOD_PRICES_EGY`).
* **FAOSTAT:** Food inflation percentages.
* **UN Comtrade:** International import volumes and USD trade values (`TradeData`).

### Star Schema Architecture:
* **Fact Tables (5):** `TradeData`, `WFP_FOOD_PRICES_EGY`, `Currency Rate`, `Inflation`, and `Minimum Wage`.
* **Dimension Tables (2):** `Master Calendar` (serving as the central time intelligence axis) and `DIM_products` (bridging international UN trade IDs to local Egyptian product IDs).
* **Relationships:** One-to-many (`1:*`) relationships enabling seamless cross-filtering across all four dashboard pages.

---

## ⚙️ Data Preparation (ETL Process)
1. **Stage 1 — Wide-to-Long Transformation:** Unpivoted 71 columns spanning 1960–2025 into a normalized long format using Power Query.
2. **Stage 2 — Standardization & ID Mapping:** Standardized percentage formats and mapped UN international trade codes to local Egyptian product IDs.
3. **Stage 3 — Filtering & Quality Assurance:** Removed irrelevant columns, filtered the analytical scope to 2020–2024, and validated row counts.

---

## 🧮 Core DAX Measures & Predictive Simulation

### 1. Income Erosion Index
Measures the percentage of the monthly minimum wage consumed by staple food items:
```dax
Income Erosion Index = 
DIVIDE(
    [Avg Local Price] * 30, 

    Units Affordable = 
AVERAGEX(
    VALUES('wfp_food_prices_egy'[Product]), 
    DIVIDE(
        AVERAGE('Minumum wage'[Monthly_Minimum_Wage_EGP]), 
        [Avg Local Price], 
        0
    )
)
FX Devaluation YoY % = 
VAR RatePY = CALCULATE([Avg Exchange Rate], PREVIOUSYEAR('Master Calendar'[date])) 
RETURN 
DIVIDE([Avg Exchange Rate] - RatePY, RatePY, 0)
Simulated Price (EGP) = [Avg Local Price] * (1 + (CurrencyShock * ERPT))
    AVERAGE('Minumum wage'[Monthly_Minimum_Wage_EGP]), 
    0
)
```

🖥️ Dashboard Architecture (4 Pages)PageDashboard Page TitleCore Analytical FocusPage 1The Macro Shock Catalyst   Examines the macroeconomic context, tracking how EGP devaluation (from 15.75 to 45.29 EGP/USD) transmitted into Headline CPI and food inflation.   Page 2Architecture: Sectorial Transmission (Food vs. Economy)   Identifies the most volatile commodities, survival basket growth, and commodity risk status flags (Stable, Warning, Hyper-Toxic).   Page 3Household Reality (Wages vs. Real Erosion)   Evaluates who is most impacted by comparing nominal minimum wage increases against real purchasing power erosion and physical units lost.   Page 4Sovereign Trade Vulnerabilities   Investigates supply chain vulnerabilities, total import expenditure in USD vs. EGP, and single-source partner concentration risks.   

📈 Key InsightsFood Inflation Outpaced Headline CPI by Nearly 2x: In 2023, Headline CPI reached 33.88% while food inflation surged to 63.57% — a 29.69 percentage-point gap.   Critical Commodity Spikes: The survival basket YoY price growth hit 86.29% in 2023, with critical commodities jumping from 1 to 11 (including a +96.60% spike in Sugar prices).   Severe Household Income Erosion: In 2023, a single month's supply of key staples consumed massive portions of a minimum-wage household's income: 76.08% for Farm Chicken, 69.93% for Maize Oil, and 61.37% for Sunflower Oil.   The Double Shock & Affordability Crash: Average commodity affordability crashed by -34.6% in 2023 alone. Despite the nominal minimum wage tripling from 2,000 to 6,000 EGP, overall purchasing power (Units Affordable) fell from 303 units in 2021 to 258 units in 2024.   Import Bill Explosion: Total food import expenditure surged by +635%, rising from 16.2 Billion EGP in 2020 to 119.2 Billion EGP in 2024, even as global cost per ton dropped from $1.05 to $0.98.   Single-Source Supply Chain Vulnerability: Brazil dominates Egypt's agricultural import volume at 2.25 Billion MT, ahead of Australia (1.41B MT) and Russia (1.38B MT), creating significant sovereign trade-partner concentration risk.   💡 Strategic Policy RecommendationsPillar 1 — Food Inflation Rebate Program: Automatically credit minimum-wage citizens' accounts whenever the Income Erosion Index exceeds 15%, directly cushioning severe shocks like the 76.08% Farm Chicken erosion.   Pillar 2 — Sovereign FX Hedging & Settlement: Lock in global prices via forward contracts for top imports—specifically Sunflower Oil ($2.2B) and Sugar ($1.87B)—and pursue local currency trade agreements with Brazil to bypass USD exposure.   Pillar 3 — Import Diversification & Local Production: Mandate a 25% single-country agricultural import cap to diversify supply chains away from Brazil, Australia, and Russia, while directing domestic subsidies toward Sugar, Farm Chicken, and Eggs.   👥 Project Team (DEPI Round 4 — Team 3)   Team Members: Omar Sherif, Abdolrahman Ashraf, Ahmed Mohamed, Ahmed Essam, Omar Ashraf.   Supervisor: Eng. Mahmoud Seraj | Technical Partner: CLS Learning Solutions (July 2026).   
