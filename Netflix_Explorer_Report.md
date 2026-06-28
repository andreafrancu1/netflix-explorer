
# Netflix Explorer Project Report

## Overview

Netflix Explorer is a data exploration project using Netflix-style movie, user, and viewing session data. The goal of this project is to practice an end-to-end data science workflow, including data cleaning, exploratory analysis, SQL-style analysis, statistical testing, and dashboard development.

## Project Goal

The main goal is to understand viewing behavior and content performance using product-style metrics such as watch duration, progress percentage, completion rate, and user engagement across different content types and genres.

Future analysis will focus on answering questions such as:

* Which content types have the highest average watch progress?
* Which genres drive the longest watch duration?
* Do Netflix originals perform differently from non-original content?
* How does engagement vary by user segment or subscription plan?

## Dataset Summary

The project uses three related datasets:

| Dataset  | Description                                                                                                                                |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Movies   | Content metadata including title, content type, genre, release year, duration, rating, language, country, budget, revenue, and IMDb rating |
| Users    | User information including age, gender, country, household size, subscription plan, and monthly spend                                      |
| Sessions | Viewing behavior including user ID, movie ID, user rating, watch duration, and progress percentage                                         |

Together, these datasets allow movie-level, user-level, and session-level analysis.

## Work Completed So Far

Completed project steps include:

* Imported and inspected all datasets
* Checked dataset shape, data types, summary statistics, duplicates, and missing values
* Removed duplicate records where needed
* Created helper functions for reusable plotting
* Visualized categorical and numerical feature distributions
* Handled missing values using column-specific imputation strategies
* Added missingness flags for imputed columns
* Verified before and after null counts after imputation

## Data Cleaning Summary

Missing values were handled case by case rather than using one global strategy. The imputation approach depended on the meaning of each feature, the amount of missing data, and whether related columns could be used to derive missing values.

Examples of cleaning decisions:

* Season and episode counts were filled with 0 for non-series content because those missing values were structural.
* Budget and revenue values were filled using grouped medians to reduce the impact of outliers.
* Missing secondary genres were filled with `Unknown`.
* Missing gender values were filled with `Prefer not to say` rather than inferred.
* Watch duration and progress percentage were derived from each other when possible.
* Missingness flags were added to preserve information about which values were originally missing.

## EDA Highlights

The initial exploratory analysis focused on understanding distributions across categorical and numerical features.

Current EDA areas include:

* Content type distribution
* Genre distribution
* Release year distribution
* Runtime and duration patterns
* IMDb rating distribution
* User age distribution
* Monthly spend by subscription plan
* Watch duration and progress percentage distributions

## Next Phase: SQL-Style Product Analysis

The next phase of the project is SQL-style analysis using joins, groupbys, and aggregations.

Planned questions:

* Which content types have the highest average watch progress?
* Which genres have the longest average watch duration?
* Which genres have the most completed sessions?
* Do Netflix originals have higher engagement than non-original content?
* How does engagement vary by subscription plan?
* Which user segments watch the most content?

## Future Work

Planned future work includes:

* Statistical analysis using t-tests, ANOVA, and guardrail metrics
* Product-style metric development
* Final insights and recommendations
* Interactive dashboard using Streamlit or Plotly
* Public dashboard deployment

## Technical Notebook

The full notebook contains the detailed code, cleaning logic, and exploratory analysis steps.
