# netflix-explorer
Netflix data exploration (work in progress)

This repo is actively being built.
I’m building this project step by step to simulate a real DS workflow. Here’s what’s done and what’s coming next:

- [x]  Create GitHub repo & initial README
- [x]  Import CSVs with pd.read_csv()
- [x]  Run initial EDA (head, info, describe, null checks)
- [x]  Check for and remove any duplicate data
- [x]  Check for missing values and handle data imputation case by case
- [x]  Create helper functions for plotting (plot_box(), plot_pie())
- [x]  Visualize categorical and numerical feature distributions
- [ ]  Write SQL-style queries (joins, groupbys, aggregations)
- [ ]  Apply statistical analysis (t-test, ANOVA, guardrails)
- [ ]  Design dashboard / visual storytelling (Plotly or Streamlit)
- [ ]  Final write-up with insights + polished portfolio


## Data Imputation

### Movies DataFrame
| Column | Missing % | Imputation Strategy | Rationale |
|:--|:--:|:--|:--|
| number_of_seasons   |  0.72 | Fill with 0 for movies, 1 for Limited Series, median fill rest | Missing because not all are series |
| number_of_episodes  |  0.70 | Fill with 0 for movies, median fill rest | Missing because not all are series |
| box_office_revenue  |  0.68 | Median fill group by type and genre | Median rather than mean to avoid skew from large revenue movies | 
| production_budget   |  0.65 | Median fill group by type and genre | Median rather than mean to avoid skew from large budget movies | 
| genre_secondary     |  0.64 | Fill with 'Unknown' | Preserve structure without losing rows | 
| imdb_rating         |  0.14 | Use avg session rating from user df | Average fill ok since this range is 1-5 |

### Users DataFrame
| Column | Missing % | Imputation Strategy | Rationale |
|:--|:--:|:--|:--|
| household_size  |  0.15 | Median fill group by country and subscription plan | Larger households typically have higher plans |
| age             |  0.12 | Median fill group by country and subscription plan, clipping to [13, 95] | Avoids negatives/outliers |
| monthly_spend   |  0.10 | Log-median group by subscription plan | Handles skew & reflexs tier pricing |
| gender          |  0.08 | Fill with 'Prefer not to say' | Avoids incorrect imputation, already a categorical option |

### Sessions DataFrame
| Column | Missing % | Imputation Strategy | Rationale |
|:--|:--:|:--|:--|
| user_rating             |  0.80  | Fill with neutral 3 | Most users don't rate unless they love or hate |
| watch_duration_minutes  |  0.12  | Derived from progress_percentage * duration_minutes / 100, then median fill rest | Leverages available info |
| progress_percentage     |  0.08  | Derived from watch_duration_minutes / duration_minutes * 100 | Leverages available info |

### General Practice
- Added _was_missing flags for all imputed columns
- Used median rather than mean to reduce outlier bias / skew
- Performed group-based fills when there was useful context
- Verified before/after NA counts at each step
