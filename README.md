# Masters Eligibility Analytics Dashboard

## Problem
Assessing candidate eligibility for postgraduate program admissions is a manual, error-prone process when done from raw applicant data. This project builds an interactive Power BI dashboard — "UoM Master's Eligibility Summary" — that automates eligibility assessment for the Master of Business Analytics program from a raw candidate CSV dataset (academic qualifications, professional experience, and pay verification).

## Approach
- **Data cleaning & wrangling:** Parsed and split nested academic and experience fields (institute, degree, dates, class; company, position, dates) from a single semi-structured column into clean, structured columns
- **Standardization:** Normalized institute names, degree/qualification names, and text casing (e.g. unifying "CIMA", "CIMA Sri Lanka" → "CIMA"); handled nulls and removed duplicates
- **Classification:** Grouped qualifications into categories (Honors Degree, 4-Year Degree, 3-Year Degree, Professional Qualification), and institutes by geographic location
- **DAX-driven eligibility engine:** Built calculated columns to determine qualification duration, earliest completion (effective) date, and post-qualifying work experience, then applied a 6-category eligibility ruleset:
  - Direct Eligibility (Honors Business degree from UoM; 4-year Business degree)
  - Eligible with Experience (4-year non-business degree + 1yr experience; 3-year degree + 2yrs experience)
  - Eligible (recognized professional qualification, e.g. CIMA, + 2yrs experience)
  - Special Admission (Senior Managers/Entrepreneurs, capped at 10% of class size)
  - Not Eligible
- **Dashboard design:** Built a 3-page interactive dashboard with slicers, key visuals (pie, funnel, and stacked bar charts) to let stakeholders explore eligibility status dynamically

## Tools
Power BI (Power Query, DAX), data cleaning & wrangling

## Outcome
An interactive dashboard that turns a raw, semi-structured applicant dataset into an automated eligibility assessment tool — replacing manual review with a rule-based classification system stakeholders can filter and explore directly.

## Artifacts

### Dashboard Overview
![Dashboard Overview](https://github.com/Imagunaratne/Master-s-Eligibility-Analytics-Dashboard/blob/35c8583d80935d21a3e8ceebe3850e64b77fb15a/Dashboard%20SS%201.png)

