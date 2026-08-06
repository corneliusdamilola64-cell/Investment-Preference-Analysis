# Investment Preference & Behaviour Dashboard — WealthBridge Advisors

> Turning investor survey data into a decision-ready Power BI dashboard.

![Dashboard Preview](visuals/DASHBOARD.png)

![Power BI](https://img.shields.io/badge/Power%20BI-Data%20Visualization-F2C811?logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-Power%20Query-217346?logo=microsoftexcel)
![DAX](https://img.shields.io/badge/DAX-Measures-blue)

🔗 **[View the live interactive dashboard →](#)** *(replace # with your published Power BI link)*

---

## Executive Summary

WealthBridge Advisors wanted to understand how demographics, goals, and risk appetite shape investment decisions. I cleaned and modeled survey data from 40 investors in Excel Power Query, built the data model and DAX measures in Power BI, and delivered an interactive dashboard the team can filter by age, gender, and investment goal.

**The key finding:** respondents said "returns" mattered most to them — but the investment avenue they actually put the most money into was PPF, a low-risk option. What people say they value and what they actually choose weren't the same thing, which changes how WealthBridge should message its products.

---

## Business Problem

WealthBridge had survey data sitting in a spreadsheet with no structured way to answer basic questions about their client base — which investments people preferred, which segments were most active, and what was actually driving decisions. This project turned that raw data into something the team could filter, explore, and act on.

## Business Questions

1. Which investment avenue is most preferred?
2. Which age group invests the most?
3. Does gender influence investment behaviour?
4. Which factor drives investment decisions?
5. What investment duration is most common?
6. Which customer segment should the firm target?

---

## Data Preparation (Excel Power Query)

- Imported and standardized raw survey data
- Corrected spelling/labeling inconsistencies across categorical fields *(e.g. "PPF", "P.P.F", "ppf" → one consistent label)*
- Handled missing values: *[state your actual method here — e.g. "3 rows with missing income data were removed; 2 blank duration fields were imputed with the column mode"]*
- Created an `Age Group` column via conditional binning for segment analysis
- Converted data types (dates, categorical, numeric) to support accurate DAX aggregation

## Data Model

Single flat table, 40 respondents. No relational model was needed for this dataset — every field lives at the respondent grain, so segmentation is done through DAX rather than joins.

---

## DAX Measures

```dax
Total Investors = 
DISTINCTCOUNT('Survey'[RespondentID])
```

```dax
Most Preferred Investment = 
VAR RankedInvestments =
    TOPN(
        1,
        SUMMARIZE(
            'Survey',
            'Survey'[InvestmentAvenue],
            "InvestorCount", DISTINCTCOUNT('Survey'[RespondentID])
        ),
        [InvestorCount], DESC
    )
RETURN
    MAXX(RankedInvestments, 'Survey'[InvestmentAvenue])
```

```dax
Top Decision Factor = 
VAR RankedFactors =
    TOPN(
        1,
        SUMMARIZE(
            'Survey',
            'Survey'[DecisionFactor],
            "FactorCount", DISTINCTCOUNT('Survey'[RespondentID])
        ),
        [FactorCount], DESC
    )
RETURN
    MAXX(RankedFactors, 'Survey'[DecisionFactor])
```

*(Full measure list — including `Average Age` and `Preferred Investment Duration` — follows the same rank-and-select pattern and is included in the .pbix file.)*

---

## Key Insights

**Returns vs. Reality** — Returns ranked #1 as a stated decision factor, but PPF (a capital-safety instrument) received the highest actual allocation. Stated preference and revealed preference diverged.

**Core Segment** — The 26–30 age group was the largest and most active investor segment in the sample.

**Gender Split** — Male respondents participated more across most investment avenues; *[add the actual % split once confirmed from your data]*.

**Investment Goals** — Retirement planning was the dominant stated objective, with a preferred holding duration of 3–5 years.

---

## Recommendations

- **Target the 26–30 segment** specifically — they make up the largest share of active investors in this sample.
- **Lead with returns messaging, but pair it with risk clarity** — since actual behaviour skews toward safety, products that promise returns *and* explicitly de-risk will likely convert better than returns-only messaging.
- **Design medium-term products (3–5 years)** around retirement goals rather than short-term trading products.
- **Build separate campaigns by demographic segment** rather than one blanket campaign, since decision drivers differ across groups.

---

## Business Impact

This dashboard gives WealthBridge Advisors a repeatable way to:

- Spot the gap between what clients say and what they do, and adjust messaging accordingly
- Identify and prioritize the highest-value client segment
- Base product and campaign decisions on evidence instead of assumption

---

## Tools & Approach

| Category | Tool |
|---|---|
| Data Cleaning | Excel (Power Query) |
| Data Modeling & Analysis | Power BI |
| Calculations | DAX |

My background is in Industrial Chemistry, which shapes how I approach analysis: question the data before trusting it, look for contradictions between what a dataset claims and what it shows, and make sure every insight can be explained and defended — not just visualized.

---

## Repository Structure

```text
investment-preference-dashboard/
├── data/
│   ├── raw/
│   └── processed/
├── docs/
├── reports/
├── visuals/
└── README.md
```

## Deliverables

- Power BI dashboard (.pbix)
- Cleaned dataset
- Executive summary
- Business questions & answers

---

## About the Author

**Damilola Cornelius**
Data Analyst | Power BI Developer

- GitHub: *[add your GitHub profile link]*
- LinkedIn: *[add your LinkedIn profile link]*
- Portfolio: *[add your portfolio link]*
- Live Dashboard: *[add your published Power BI link]*

---

*This project is shared for portfolio purposes.*
