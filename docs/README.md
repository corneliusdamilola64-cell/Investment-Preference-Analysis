# Investment Preference & Behaviour Dashboard — WealthBridge Advisors
> Analyzed survey data from 40 investors to uncover how demographics, risk appetite, and goals shape investment decisions, delivering a Power BI dashboard and strategic recommendations for a financial advisory firm.

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Data Workflow](#5-data-workflow)
6. [Data Model & Schema](#6-data-model--schema)
7. [Analysis & Metrics](#7-analysis--metrics)
8. [Key Insights](#8-key-insights)
9. [Recommendations](#9-recommendations)
10. [Assumptions & Limitations](#10-assumptions--limitations)
11. [Future Enhancements](#11-future-enhancements)
12. [Deliverables](#12-deliverables)
13. [Author](#13-author)

---

## 1. Project Overview

**Context:** WealthBridge Advisors is a financial advisory firm offering services from mutual funds to stock market investments to fixed deposits. To grow its client base, the firm needed to understand who its potential clients are and how they make investment decisions.

**Problem Statement:** The firm collected survey responses on investment preferences, behaviors, and demographics but had no structured way to see who invests in what, why, and which factors drive those choices.

**Approach:** Survey data from 40 respondents was cleaned in Excel (Power Query), then modeled and visualized in Power BI to compare investment avenues, decision factors, savings objectives, and expected returns across gender and age groups.

**Outcome:** An interactive Power BI dashboard and executive summary showing that while investors say **Returns** matter most, actual behavior skews toward safer instruments like **PPF** — a gap between stated priorities and real allocation that has direct implications for how the firm should pitch its products.

---

## 2. Objectives

- **Primary Objective:** Determine which investment avenues different demographic groups prefer and what factors drive those decisions.
- **Secondary Objective 1:** Compare investment preferences by gender and by age group (21–25, 26–30, 31–35).
- **Secondary Objective 2:** Identify the primary factors (Returns, Risk, Locking Period) influencing decisions within each age group.
- **Secondary Objective 3:** Build a Power BI dashboard with KPIs that WealthBridge Advisors can use on an ongoing basis to track investment trends.

> 💡 *Every analysis decision in this project traces back to one of these objectives.*

---

## 3. Project Scope & Tools

### Scope

| Dimension | Details |
|-----------|---------|
| **In Scope** | Survey responses from 40 individuals covering demographics, investment avenues and amounts, decision factors, savings objectives, investment duration, expected returns, and information sources. |
| **Out of Scope** | Actual portfolio performance data and longitudinal tracking were excluded — the survey captures a single point-in-time snapshot of stated preferences, not verified behavior over time. |
| **Time Period** | Single survey snapshot (no date range in the underlying data). |
| **Granularity** | One row per survey respondent. |

### Tools & Technologies

| Category | Tool(s) Used |
|----------|-------------|
| Data Storage | CSV / Excel |
| Data Processing | Excel (Power Query) |
| Analysis | Power BI (DAX measures, interactive visuals) |
| Visualization | Power BI |
| Documentation | Markdown, Word |

---

## 4. Repository Structure

```
investment-preference-dashboard/
│
├── data/
│   ├── raw/                  # Original survey export - never edited
│   └── processed/            # Cleaned dataset used in Power BI
│
├── reports/                  # Executive summary, business question answers
│
├── visuals/                  # Dashboard screenshot
│
├── docs/                     # Data dictionary / column definitions
│
└── README.md                 # You are here
```

> ⚠️ *Folders not used by this project (queries/, notebooks/, scripts/) have been removed — this was a Power BI + Excel project, not a coding or SQL project.*

---

## 5. Data Workflow

```
[Survey CSV Export]
      ↓
[Ingestion into Excel]
      ↓
[Cleaning & Transformation - Power Query]
      ↓
[Analysis / Visualization - Power BI]
      ↓
[Dashboard + Executive Summary]
```

1. **Source:** Survey data collected by WealthBridge Advisors on investment preferences, behaviors, and demographics.
2. **Ingestion:** Loaded into Excel for cleaning via Power Query.
3. **Cleaning:** Standardized column headers, renamed "What are your savings objective?" to "Savings Objective", corrected "Stock Marktet" to "Stock Market", and handled missing values (numeric columns filled with 0/average, text columns filled with "Not Specified").
4. **Transformation:** Created an **Age Group** field bucketing respondents into 21–25 (Early Adulthood), 26–30 (Established Adulthood), and 31–35 (Experienced Adulthood).
5. **Analysis:** Cross-tab segmentation and comparison in Power BI — investment preference by gender, by age group, decision factors by age group, savings objectives by duration, and mutual fund reasons by expected return.
6. **Output:** Interactive Power BI dashboard, cleaned dataset, and a one-page executive summary for firm leadership.

---

## 6. Data Model & Schema

### Dataset: Investment Preference Survey

| Field Name | Data Type | Description | Example Value |
|------------|-----------|-------------|---------------|
| `gender` | string | Gender of the respondent | "Male" |
| `age` | int | Age of the respondent | 28 |
| `Age_Group` | string | Derived age bucket | "26-30 Established Adulthood" |
| `Investment_Avenues` | boolean | Whether the respondent invests in a given avenue | "Yes" |
| `Mutual_Funds`, `Equity_Market`, `Debentures`, `Government_Bonds`, `Fixed_Deposits`, `PPF`, `Gold` | float | Amount invested in each avenue | 15000 |
| `Stock_Market` | boolean | Whether the respondent invests in the stock market | "Yes" |
| `Factor` | string | Primary factor influencing investment decisions | "Returns" |
| `Objective` | string | Main objective for investing | "Growth" |
| `Purpose` | string | Purpose of investments | "Wealth Creation" |
| `Duration` | string | Investment duration | "3-5 years" |
| `Invest_Monitor` | string | Frequency of monitoring investments | "Monthly" |
| `Expect` | string | Expected returns from investments | "20%-30%" |
| `Avenue` | string | Preferred avenue for investments | "Mutual Fund" |
| `Savings_Objective` | string | Primary savings objective | "Retirement Plan" |
| `Reason_Equity`, `Reason_Mutual`, `Reason_Bonds`, `Reason_FD` | string | Reason for choosing each avenue | "Better Returns" |
| `Source` | string | Source of investment information | "Financial Consultants" |

> **Row count:** 40 respondents
> **Structure:** Single flat table — no joins or relational schema; not a SQL project.

---

## 7. Analysis & Metrics

### Analytical Approach

This was exploratory, descriptive analysis: segmenting a single survey dataset by demographic and behavioral dimensions to surface patterns in investment preference and decision-making, rather than testing a formal hypothesis or building a predictive model.

### Key Metrics Defined

| Metric | Plain-Language Definition | Why It Matters |
|--------|--------------------------|----------------|
| Investment Preference by Gender | Number of investors choosing each avenue, split by gender | Shows which products to market differently to male vs. female investors |
| Investment Preference by Age Group | Number of investors choosing each avenue, split by age bucket | Identifies which age segment is most active and in which products |
| Decision Factor by Age Group | Count of investors citing Returns, Risk, or Locking Period as their top factor, by age group | Reveals what messaging (returns vs. safety) resonates with each segment |
| Savings Objective by Duration | Count of investors per savings objective, split by investment duration | Links long-term goals (e.g., retirement) to product tenor |

### Methods Used

- Descriptive statistics (counts, averages — e.g., average investor age)
- Segmentation / group comparison by gender and age group
- Cross-tabulation of savings objective against investment duration
- Cross-tabulation of mutual fund reasons against expected return bracket
- KPI cards for at-a-glance metrics (Total Investors, Average Age, Top Investment, Key Driver, Preferred Duration)

---

## 8. Key Insights

**Insight 1: Stated priorities don't match actual allocation**
Investors ranked **Returns** as the top factor influencing their decisions, yet **PPF** — a low-risk, low-return instrument — was the most-invested-in avenue overall. This suggests investors talk about return-seeking behavior but actually allocate toward safety and capital preservation.

**Insight 2: Male investors are more active across most avenues**
Male respondents recorded higher investment participation than female respondents across nearly every investment avenue, indicating an engagement gap the firm could address through targeted outreach.

**Insight 3: The 26–30 age group is the core client segment**
"Established Adulthood" (26–30) investors were both the largest group and the most active across investment avenues, positioning them as the firm's primary growth segment.

**Insight 4: Retirement planning drives medium-term investing**
**Retirement Planning** was the dominant savings objective, concentrated among investors with a **3–5 year** investment horizon — the most preferred duration overall.

**Insight 5: Return expectations shape mutual fund appeal**
Investors expecting **20%–30% returns** showed the strongest interest in mutual funds, primarily for **Better Returns**, making this expectation bracket the clearest target for mutual fund products.

---

## 9. Recommendations

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
| High | Build targeted campaigns for the 26–30 (Established Adulthood) segment, the largest and most active investor group. | Insight 3 | Marketing / Client Acquisition |
| High | Lead product messaging with potential returns while clearly disclosing risk, since Returns is the top-cited decision factor even though behavior skews toward safer products. | Insight 1 | Product Marketing / Advisory |
| Medium | Design and promote products aligned with 3–5 year horizons framed around retirement planning. | Insight 4 | Product Team |
| Medium | Tailor marketing and advisory outreach separately for male and female investors to close the engagement gap. | Insight 2 | Client Advisory |

---

## 10. Assumptions & Limitations

### Assumptions
- Survey responses were assumed to be complete and accurate as self-reported by respondents.
- "Age Group" buckets (21–25, 26–30, 31–35) were treated as the firm's intended segmentation for the client base.

### Limitations
- Sample size is small (40 respondents), limiting how confidently findings generalize to the firm's full target market.
- Data reflects a single point-in-time survey, not verified or longitudinal investment behavior.
- Investment amounts are self-reported and not cross-checked against actual account or portfolio data.

> *The goal here is pre-emptive Q&A: a thoughtful skeptic would ask about sample size and self-reported data first — both are addressed above.*

---

## 11. Future Enhancements

- [ ] Expand the survey sample beyond 40 respondents to improve statistical confidence in segment-level findings.
- [ ] Track the same investor cohort over time to see whether stated priorities (e.g., Returns) start to match actual allocation.
- [ ] Cross-reference survey responses with real portfolio data where available, to validate self-reported amounts.
- [ ] Add a predictive segmentation model to score new leads by likely product fit.

---

## 12. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| Dashboard Screenshot | Power BI dashboard covering all required visuals and KPIs | `visuals/DASHBOARD.png` |
| Cleaned Dataset | Standardized, missing-value-handled survey data | `data/processed/CLEANED_DATA.xlsx` |
| Executive Summary | One-page, 300–500 word summary for firm leadership | `reports/EXECUTIVE_SUMMARY.docx` |
| Business Questions & Answers | Answers to the six required analysis questions | `reports/Data_Analysis_Stage_5.pdf` |

---

## 13. Author

**[Your Name]**
Data Analyst

- 🔗 [LinkedIn URL]
- 💼 [Portfolio or GitHub profile URL]
- 📧 [Email - optional]

---

*Last updated: August 2026*
