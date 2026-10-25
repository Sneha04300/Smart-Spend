
#Smart Spend — Retail Spending Intelligence & Decision Support

An Advanced Data Science Project using the BADIR Framework

<p align="center">

Turning Retail Transaction Data into Actionable Business Insights

</p>

1. Project Overview

Smart Spend is a data-driven retail analytics and decision-support project designed to analyse purchasing behaviour, customer spending patterns, product performance, and transaction trends.

The project aims to transform large-scale retail transaction data into meaningful insights that help retail businesses make informed decisions about customer retention, promotions, inventory planning, and sales strategies.

Using data engineering, exploratory data analysis, statistical hypothesis testing, feature engineering, and appropriate machine learning techniques, Smart Spend will follow the complete data science lifecycle.

The project follows the BADIR framework:

B — Business Question

A — Analysis Plan

D — Data Collection

I — Insights

R — Recommendations

The project is being developed as part of the Advanced Data Science course.

2. Problem Statement

Retail businesses generate large volumes of transaction data containing information about products, quantities, prices, purchase dates, customers, and locations. However, raw transactional records do not directly explain customer behaviour or provide clear guidance for business decisions.

Retailers may struggle to identify valuable customer segments, understand seasonal purchasing patterns, evaluate product performance, and recognise transaction cancellation trends.

Smart Spend aims to address this problem by integrating retail transaction data with relevant calendar information, engineering meaningful analytical features, and applying data science techniques to derive actionable business insights.

Key Business Objectives

Analyse retail spending and purchasing patterns over time.

Identify high-value, frequent, and inactive customer segments where customer identifiers are available.

Evaluate product performance using sales value and quantity-based metrics.

Investigate cancellation patterns and their relationship with products, dates, and customer segments.

Examine differences in purchasing behaviour around relevant public holidays.

Develop evidence-based recommendations for customer retention, promotions, and business planning.

Build a reproducible analytical workflow and, where feasible, a decision-support dashboard.

3. Stakeholder and Decision Context

Primary stakeholder: Retail business managers and sales or marketing teams.

Business decisions supported:

Which customer segments may benefit from targeted promotions?

Which products contribute most to recorded sales value?

When do purchasing patterns change?

Are cancellations concentrated in particular products or customer segments?

Do transaction values differ between public holidays and non-holiday dates?

Which areas should be prioritised for further investigation?

The project will distinguish observed associations from causal effects. Recommendations will be based on validated findings rather than assumptions.

4. Dataset Requirements

The planned integrated dataset must satisfy the following project requirements:

Requirement

Target

Minimum number of transaction rows

100,000 valid rows

Minimum number of meaningful variables

40

Number of data sources

Multiple documented sources

Integration approach

Reproducible ETL pipeline

Master dataset

Single Source of Truth (SSOT)

Data quality

Documented cleaning and validation

Analytical approach

EDA, hypothesis testing and suitable advanced analytics

These are project targets. Final row counts, variable counts, missing-value statistics, and validation results will be documented after implementation.

5. Data Sources

Dataset 1: Online Retail II

Source: UCI Machine Learning Repository

Official link: https://archive.ics.uci.edu/dataset/502/online+retail+ii

Online Retail II contains historical transaction records from a UK-based online retailer, covering December 2009 through December 2011.

The published dataset contains approximately 1,067,371 transaction records and eight original fields.

Original field

Purpose

Invoice

Transaction identification and cancellation investigation

StockCode

Product identification

Description

Product description

Quantity

Number of units recorded

InvoiceDate

Transaction date and time

Price

Unit price

Customer ID

Customer-level analysis where available

Country

Geographic analysis

This dataset will provide the primary transaction-level information for Smart Spend.

Dataset 2: UK Bank Holidays

Source: UK Government

Official link: https://www.gov.uk/bank-holidays.json

The supplementary dataset provides public-holiday information, including dates, holiday names, and regional information.

It will be used to derive relevant calendar features and investigate whether purchasing patterns differ around applicable public holidays.

Only dates and regions relevant to the transaction data will be used. The analysis will account for the historical coverage of the retail dataset.

Dataset Selection Rationale

The primary dataset supplies transaction-level information, while the supplementary source adds calendar context.

The sources will be combined only after inspecting their schemas, validating date formats, documenting their provenance, and confirming that the integration is analytically appropriate.

The supplementary dataset does not independently satisfy the 100,000-row requirement. That requirement will be assessed against the integrated transaction-level master dataset.

6. Data Integration and Single Source of Truth (SSOT)

The project will use a reproducible Extract, Transform, Load (ETL) workflow.

Integration Workflow

Extract the retail transaction data and supplementary calendar data.

Inspect schemas, data types, source coverage, and data quality.

Standardise transaction dates and calendar dates.

Investigate duplicate records and missing values.

Identify cancellation records and define appropriate sales calculations.

Prepare the holiday table with relevant dates and regions.

Join relevant calendar information to transaction records using transaction date and regional applicability.

Validate join cardinality and ensure the join does not unintentionally multiply transaction rows.

Engineer meaningful transaction, customer, product, and calendar variables.

Validate the resulting master dataset and document all transformations.

Data Quality Checks

Missing-value analysis

Duplicate-record investigation

Date and data-type validation

Quantity and price validation

Cancellation identification

Transaction-value verification

Join-key validation

Row-count reconciliation

Post-integration missingness checks

Feature-definition and leakage checks

SSOT Design

The SSOT will be the validated transaction-level master dataset used consistently across analysis and reporting.

Customer-level and product-level metrics will be derived using documented aggregation rules rather than being indiscriminately joined to every transaction.

Raw source data will be preserved separately where permitted, and transformations will be reproducible through code.

7. Feature Engineering: 40+ Meaningful Variables

The original retail dataset contains eight fields. Additional analytical variables will be engineered based on their relevance to the business questions.

Planned feature categories include:

A. Transaction Features

Transaction value

Absolute transaction quantity

Transaction hour

Day of week

Day of month

Month

Quarter

Year

Weekend indicator

Relevant holiday indicator

B. Customer Features

Where customer identifiers and sufficient historical records are available:

Total recorded spend

Total purchase frequency

Average order value

Median order value

Most recent purchase date

Days since last purchase

Unique products purchased

Average quantity per order

Repeat-purchase indicator

Customer tenure within the observed data

Customer purchase interval

Customer spending variability

C. Product Features

Total recorded quantity sold

Total recorded sales value

Average unit price

Median unit price

Number of distinct invoices

Number of purchasing customers

Average quantity per invoice

Product sales rank

Product price variability

Product demand variability

D. Calendar and Behavioural Features

Holiday name

Applicable holiday region

Days until the next relevant holiday

Days since the previous relevant holiday

Month-over-month sales change

Quarter-level sales change

Customer purchase recency category

Customer frequency category

Customer monetary-value category

Cancellation indicator

The final feature list will include a data dictionary with each variable's definition, data type, calculation method, business relevance, and missing-value treatment.

Important: The features above are proposals, not a claim that 40 validated variables already exist. The final number of meaningful variables will be verified after engineering and data-quality checks. Features that are redundant, unsupported, or unsuitable for the analysis will not be added merely to inflate the count.

8. Research Questions and Hypotheses

Research Question 1: Spending Across Weekdays

Question: Does average transaction value differ across weekdays?

Null hypothesis (H0): Mean transaction values are equal across weekdays.

Alternative hypothesis (H1): At least one weekday has a different mean transaction value.

Potential method: ANOVA if assumptions are sufficiently satisfied, or an appropriate non-parametric alternative.

Research Question 2: Cancellation Patterns

Question: Are cancellation rates associated with product or customer segments?

H0: Cancellation status is independent of the selected categorical segment.

H1: Cancellation status is associated with the selected segment.

Potential method: Chi-square test of independence, with suitable handling of small expected cell counts.

Research Question 3: Repeat Customers and Order Value

Question: Do repeat customers and one-time customers have different average order values?

H0: The groups have equal average order values.

H1: The groups have different average order values.

Potential method: An appropriate two-group statistical test, with the unit of analysis and assumptions clearly defined.

Research Question 4: Holiday-Related Spending

Question: Does transaction value differ between relevant public holidays and non-holiday dates?

H0: There is no difference in the selected transaction-value measure between the two groups.

H1: The selected measure differs between the groups.

Potential methods include an appropriate two-group test and regression with relevant controls.

These hypotheses will be evaluated using suitable statistical tests, effect sizes, and confidence intervals. Multiple testing and dependence between transactions will be considered where relevant.

9. BADIR Framework

Smart Spend will follow all five BADIR stages.

B — Business Question

Identify the stakeholder and decision context.

Define the business problem.

Formulate research questions and hypotheses.

Define business KPIs and success criteria.

Expected output: Business problem statement, research questions, hypotheses, and KPI definitions.

A — Analysis Plan

Map each research question to a suitable analytical method.

Specify data requirements and assumptions.

Define statistical tests and evaluation metrics.

Plan visualisations and validation procedures.

Expected output: Documented analysis plan and validation strategy.

D — Data Collection

Acquire and document datasets.

Inspect schemas and data quality.

Clean and integrate sources.

Engineer and validate meaningful variables.

Create the SSOT.

Expected output: Reproducible data pipeline, data dictionary, and quality report.

I — Insights

Perform exploratory data analysis.

Examine relationships and distributions.

Conduct hypothesis testing.

Apply suitable segmentation or predictive modelling.

Evaluate models and explain important results.

Expected output: Evidence-backed insights, statistical results, and analytical visualisations.

R — Recommendations

Translate results into business actions.

Prioritise recommendations by expected value and feasibility.

Explain uncertainty and limitations.

Develop a decision-support report or dashboard.

Expected output: Actionable recommendations and a reproducible final project deliverable.

10. Analytical Methodology

Exploratory Data Analysis (EDA)

Dataset dimensions and schema inspection

Missing-value and duplicate analysis

Descriptive statistics

Transaction-value distributions

Sales trends by date and product

Customer purchase-frequency analysis

Country-level comparisons

Cancellation-pattern analysis

Correlation and association analysis where appropriate

Statistical Analysis

Hypothesis tests will be selected based on variable types, sampling assumptions, distributional characteristics, and the research questions.

Results will include appropriate test statistics, p-values, confidence intervals, and effect sizes where applicable.

Customer Segmentation

Potential customer features include recency, frequency, and monetary value (RFM).

Segmentation methods may include rule-based RFM groups or clustering techniques, subject to data suitability and validation.

Predictive Analytics

A predictive task will be selected only when it is justified by the available data and business objective.

Potential tasks include customer-segment classification or sales-related forecasting. Evaluation will use suitable holdout data, task-specific metrics, and leakage prevention.

No predictive model or performance score will be reported until it has been implemented and evaluated.

11. Responsible and Explainable AI

The project will consider:

Data provenance and permitted use

Privacy and responsible handling of customer identifiers

Missing-data and selection biases

The limitations of historical retail records

Explainability of segmentation and predictive results

Appropriate use of SHAP or other explanation methods if a suitable predictive model is implemented

The difference between correlation and causation

Clear communication of uncertainty and limitations

The analysis will avoid treating historical customer patterns as guarantees of future behaviour.

12. Tools and Technologies

Planned tools include:

Tool

Purpose

Python

Data processing and analysis

Jupyter Notebook

Reproducible analysis and documentation

Pandas

Data manipulation and integration

NumPy

Numerical operations

Matplotlib

Data visualisation

Seaborn

Statistical visualisation

SciPy

Statistical hypothesis testing

Scikit-learn

Suitable machine learning and evaluation

Git

Version control

GitHub

Public source-code repository

Additional tools such as MLflow, Spark, or a dashboard framework may be considered if justified by project scope and requirements.

13. Project Structure

The repository is planned to follow this structure:

Smart-Spend/
├── README.md
├── .gitignore
├── requirements.txt
├── data/
│   ├── raw/
│   ├── processed/
│   └── README.md
├── notebooks/
│   ├── 01_data_profiling.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_data_integration.ipynb
│   ├── 04_feature_engineering.ipynb
│   └── 05_analysis_and_insights.ipynb
├── src/
│   ├── data_loading.py
│   ├── data_cleaning.py
│   ├── data_integration.py
│   └── feature_engineering.py
├── reports/
│   ├── figures/
│   └── project_summary.md
└── tests/
    └── test_data_quality.py

Large raw datasets and generated files will not be committed unnecessarily. The data/README.md file will document dataset sources, download instructions, and expected filenames.

14. Project Roadmap

Phase

Planned work

Phase 1

Business understanding and BADIR planning

Phase 2

Dataset acquisition and source documentation

Phase 3

Data profiling and quality assessment

Phase 4

Data cleaning and SSOT integration

Phase 5

Feature engineering and validation

Phase 6

EDA and hypothesis testing

Phase 7

Segmentation and suitable predictive analysis

Phase 8

Explainability and responsible-AI review

Phase 9

Recommendations and dashboard/report

Phase 10

Final evaluation, documentation, and presentation

The project will progress through these phases iteratively. Completion status will be updated based on actual implementation and validation.

15. Expected Deliverables

Documented business problem and BADIR workflow.

Source-documented datasets and reproducible integration code.

Validated transaction-level SSOT meeting the row and feature requirements.

Data dictionary and data-quality report.

Reproducible Jupyter notebooks.

EDA visualisations and statistical hypothesis-test results.

Appropriate analytical or predictive models, if justified.

Explainability and responsible-AI considerations.

Evidence-based business recommendations.

Final report, presentation, and public GitHub repository.

16. Limitations

The primary dataset contains historical transactions and does not directly represent personal household expenditure.

Customer identifiers may be missing, limiting customer-level analysis.

Cancellations and negative quantities require careful interpretation.

Holiday effects may differ by year and region.

Observational associations do not establish causal relationships.

Historical patterns may not generalise to present-day retail conditions.

Feature engineering and aggregation can introduce leakage if temporal boundaries are not respected.

These limitations will be documented and addressed where possible.

17. Current Project Status

Project stage: Initial planning and repository setup.

The project title, business direction, proposed data sources, and BADIR methodology have been outlined.

The following items remain subject to implementation and verification:

Dataset acquisition and initial profiling

Data-quality assessment

SSOT integration

Validation of the 100,000-row and 40-variable requirements

Statistical analysis and hypothesis testing

Model development and evaluation, if appropriate

Final insights, recommendations, and reporting

Progress statements will be updated as each component is completed.

18. References

UCI Machine Learning Repository. Online Retail II. https://archive.ics.uci.edu/dataset/502/online+retail+ii

UK Government. Bank holidays. https://www.gov.uk/bank-holidays.json

Academic Integrity

This repository is intended for educational and academic use. Dataset sources, transformations, analytical assumptions, and limitations will be documented. All reported results will be based on the implemented and validated analysis.

Smart Spend — From Retail Data to Better Decisions.
