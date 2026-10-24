# Massachusetts Loan Default Risk & Local Economic Factors

A descriptive analytics and data integration project examining how Massachusetts loan default risk relates to both borrower-level credit characteristics and community-level socioeconomic conditions. The project combines LendingClub's 2019 loan data with U.S. Census Bureau American Community Survey (ACS) indicators at the ZIP3 level to test whether place-based factors add incremental signal beyond traditional credit features.

**Course:** Introduction to Data Analytics (MSBA, Fall 2025)
**Section / Team:** A01
**Institution:** Boston University, Questrom School of Business

## Team Members

- Kara Liao
- Sai Leela Rahul Pujari
- Juncheng (Leo) Zhu
- Sarah Dsouza
- Roberto Albornoz

## Project Overview

Financial institutions face an enduring challenge: assessing default risk on loan applications when borrower-level credit signals tell only part of the story. Traditional underwriting relies heavily on FICO scores, credit grades, and capacity-to-repay metrics, but loan performance is also shaped by the local economic environment in which borrowers live and work.

This project takes a Massachusetts-focused lens to that question. We start by cleaning and standardizing LendingClub's 2019 nationwide loan dataset (665K+ records), then filter to Massachusetts borrowers and merge with U.S. Census Bureau ACS 2019 5-Year Estimates at the ZIP3 level. The integrated dataset enables us to study both *who* the borrower is (FICO, grade, DTI, term, employment length, purpose) and *where* the borrower lives (median household income, age structure, family size, earner composition) — and to test whether community-level context refines the picture beyond what borrower features alone can explain.

The output is a 15-question exploratory analysis, supported by national, Massachusetts-specific, and geographic visualizations, that establishes the descriptive foundation for risk-based pricing and geographic concentration management.

## Objectives

- Build a Massachusetts loan-level risk view by combining LendingClub 2019 borrower features with local ACS socioeconomic indicators at the ZIP3 level.
- Quantify how credit quality (FICO, grade) and capacity-to-repay (DTI, term) drive default probability and pricing.
- Test whether community-level conditions (income, age structure) add incremental signal to borrower-level risk.

## Data Sources

- **Primary**: [LendingClub Loan Data (2019)](https://www.kaggle.com/datasets/beatafaron/loan-credit-risk-and-population-stability?select=loan_2019_20.csv) — ~665K loan records covering nationwide originations with borrower characteristics, loan terms, credit metrics, and outcome status.
- **Secondary**: [U.S. Census Bureau American Community Survey (ACS), 2019 5-Year Estimates](https://data.census.gov/table/ACSST1Y2019.S1903) — Massachusetts socioeconomic indicators including median household income, age distribution, family size, and earner composition, joined at the ZIP3 level.

Raw datasets are not included in this repository due to size and redistribution considerations; the links above point to public sources.

## Methodology

**Data preparation and cleaning**
- Standardized LendingClub fields into model-ready formats — converted string-formatted percentages to numeric, normalized employment-length strings, derived binary verification flags, encoded multi-class loan status into a binary default indicator (Charged Off / Default = 1; Current / Fully Paid / In-Grace / Late = 0), and filtered to Massachusetts borrowers.
- Cleaned the ACS dataset — fixed misaligned headers, removed margin-of-error columns, isolated estimate-only data, and extracted total households, age distribution, family size, earner counts and percentages, percent age over 65, and median household income at the ZCTA5 level.
- Aggregated ACS variables from ZCTA5 to ZIP3 to align with LendingClub's ZIP3-level borrower location field.

**Data integration**
- Performed a one-to-many join between borrower-level loan records and ZIP3-level socioeconomic indicators, producing an integrated dataset where each loan carries both its individual borrower features and the community-level context of where the borrower lives.

**Exploratory analysis**
- Conducted 15 structured EDA questions spanning national-level patterns, Massachusetts-specific comparisons, and integrated borrower-plus-geographic analyses.
- Used violin, heatmap, bar, correlation, and choropleth visualizations to surface relationships between borrower risk factors, loan outcomes, and local economic context.

## Key Findings

- **Default risk declines monotonically with higher FICO and better credit grades**, and **60-month terms consistently carry higher default probability than 36-month terms** — confirming that grade, FICO, and maturity are foundational risk signals.
- **Interest rates are inversely related to FICO and grade**, indicating that the market's risk-based pricing machinery is broadly functioning as intended. Residual rate dispersion within grade bands maps to capacity and behavior variables (DTI, purpose, revolving utilization) rather than to noise.
- **Employment length shows weak association with income** once credit quality is controlled for, suggesting that tenure is a poor proxy for ability to repay in this market.
- **Lower-income Massachusetts ZIP3s exhibit persistently higher delinquency** even after controlling for core borrower attributes, while higher-income areas perform better. Age-structure indicators show non-linear relationships consistent with labor-market and cost-of-living trade-offs.
- **Geographic context adds genuine calibration value as an overlay**, helping to explain residual risk and reduce geographic miscalibration without replacing borrower-level signals.

## Recommendations

The analysis supports three operational recommendations for lenders operating in the Massachusetts market:
- Anchor underwriting on FICO and grade, and add term-based PD uplifts to reflect longer-exposure risk on 60-month loans.
- Incorporate a simple geographic overlay (ZIP3 median income) as a tie-breaker for borderline files and for portfolio concentration limits.
- Favor smaller amounts and/or shorter terms for riskier grades, and monitor high-DTI pockets within low-income ZIP3s for early-warning signals.

## My Contribution

As a member of Team A01, my contributions to this project were:

- **Financial domain expertise and analytical interpretation.** As the team member with prior professional experience in credit analysis and structured finance (S&P Global, Scotiabank), I led the interpretation of analytical results and their translation into business-relevant findings — connecting statistical relationships to concepts familiar to credit underwriters and risk officers (probability of default, risk-based pricing, capacity-to-repay, term premium, geographic concentration risk).
- **Findings synthesis and report authorship.** I led the writing of the project's executive summary, results interpretation, and conclusions, framing the analysis in language used by financial institutions and connecting borrower-level observations to portfolio-management and underwriting implications.
- **Recommendations development.** I authored the operational recommendations section, drawing on credit-risk experience to translate descriptive findings into actionable proposals for underwriting, pricing, and portfolio concentration management.
- **Cross-functional collaboration.** I contributed alongside teammates across data cleaning, EDA, and visualization workstreams, supporting the team's coding-focused members (Sarah Dsouza and Sai Leela Rahul Pujari) on analytical direction while the project benefited from their stronger technical execution at the time.

## Tools and Technologies

- **Python** (pandas, NumPy)
- **Visualization**: matplotlib, seaborn
- **Geographic analysis**: geopandas, folium, geopy
- **Data quality**: missingno
- **Environment**: Jupyter Notebook (originally developed in Google Colab)

## Course Context

**Introduction to Data Analytics** is a foundational course in the Boston University MSBA program at the Questrom School of Business, covering the end-to-end analytical workflow: data acquisition and cleaning, exploratory data analysis, multi-source data integration, visualization, and translation of analytical findings into business-relevant insights and recommendations.

## Other Projects

- [Loan Default Risk Prediction](https://github.com/rfalbornoz/loan-default-risk-prediction): supervised ML pipeline (logistic regression, decision tree, random forest, XGBoost) on LendingClub data for New England and New York (team project); a follow-on predictive extension of this work, so the two projects together cover the descriptive-to-predictive arc on related data.
- [Mortgage Prepayment Across Rate Regimes](https://github.com/rfalbornoz/mortgage-prepayment-rate-regimes): individual capstone research paper modeling voluntary prepayment on Freddie Mac loan-level data (2018 and 2020 vintages) with a cross-regime model transfer test.
- [European Pharmaceutical R&D Analysis](https://github.com/rfalbornoz/european-pharmaceutical-rd-analysis): unsupervised learning and statistical testing on EMA drug-authorization data (team project).
