# FIFA World Cup 2022: Exploratory Match and Team Performance Analysis

## 1. Overview

This project examines match-level statistics from the FIFA World Cup 2022 to understand how scoring, possession, shooting, passing, defensive pressure, and discipline vary across the tournament and relate to goals scored and team results.

The workflow follows a standard analytical sequence: data loading and validation, data preparation, feature engineering, descriptive statistics, correlation analysis, multi-panel visualisation, team-level aggregation, and a consolidated statistical summary report.

## 2. Objectives

- Profile the dataset and verify its quality (structure, data types, missing values).
- Engineer analytical features from raw match statistics.
- Describe tournament-wide patterns in scoring, possession, shooting, and discipline.
- Examine the strength of association between performance indicators and goals scored.
- Compare performance across tournament stages.
- Build a team-level standings table and visualise relative team performance.
- Consolidate results into a concise statistical report with clear takeaways.

## 3. Dataset

| Attribute | Detail |
|---|---|
| File used in notebook | `Fifa_world_cup_matches.csv` |
| Records | 64 matches (one row per match) |
| Variables | 88 columns |
| Missing values | 0 |
| Match identifiers | `team1`, `team2`, `date`, `hour`, `category` (tournament stage or group) |

**Variable groups used in the analysis** (a subset of the 88 columns):

| Group | Variables |
|---|---|
| Scoring | `number of goals team1/team2`, `conceded team1/team2`, `assists team1`, `goal inside the penalty area team1` |
| Possession | `possession team1/team2`, `possession in contest` |
| Shooting | `total attempts team1`, `on target attempts team1` |
| Passing | `passes team1`, `passes completed team1`, `crosses completed team1` |
| Defensive | `defensive pressures applied team1`, `forced turnovers team1` |
| Discipline | `yellow cards team1/team2`, `red cards team1/team2`, `fouls against team1/team2` |

**Tournament structure in the data**

| Stage | Matches |
|---|---|
| Group stage (Groups A to H, 6 matches each) | 48 |
| Round of 16 | 8 |
| Quarter-final | 4 |
| Semi-final | 2 |
| Play-off for third place | 1 |
| Final | 1 |
| **Total** | **64** |

## 4. Tools and Libraries

**Environment:** Python in a Jupyter Notebook (exported to HTML)

**Libraries imported in the notebook**

| Library | Import statement | Type | Use in the project |
|---|---|---|---|
| pandas | `import pandas as pd` | Third-party | Data loading, cleaning, type conversion, feature engineering, and team-level aggregation |
| NumPy | `import numpy as np` | Third-party | Numerical operations |
| Seaborn | `import seaborn as sns` | Third-party | Statistical charts: histograms with KDE, box plots, scatter and regression plots, bar and count plots, correlation heatmap; colour palettes |
| Matplotlib | `import matplotlib.pyplot as plt` | Third-party | Figure and subplot layout, titles, axis formatting, annotations, and the default plotting style |
| datetime | `from datetime import datetime` | Python standard library | Date handling support alongside pandas datetime conversion |
| warnings | `import warnings` | Python standard library | Suppressing warning messages (`warnings.filterwarnings('ignore')`) for cleaner notebook output |

**Key functions and techniques used**

| Library | Examples |
|---|---|
| pandas | `read_csv`, `to_datetime`, `isnull`, `apply`, `value_counts`, `corr`, `str.replace` |
| Seaborn | `histplot`, `boxplot`, `barplot`, `scatterplot`, `regplot`, `countplot`, `heatmap` |
| Matplotlib | `subplots`, `suptitle`, `tight_layout`, `annotate`, `axvline` |

## 5. Methodology

1. **Data loading and inspection.** The match dataset was loaded with pandas, and its shape, column types, and non-null counts were reviewed.
2. **Data quality check.** A missing-value check confirmed the dataset was complete (0 missing values).
3. **Type conversion.** The `date` field was converted to datetime, and possession fields stored as percentage strings (for example, "42%") were converted to numeric values.
4. **Feature engineering.** Match-level metrics were derived, including total goals, goal difference, a high-scoring indicator, match outcome, possession difference, shooting accuracy, goal efficiency, and pass accuracy (see Section 6).
5. **Descriptive statistics.** Tournament-level summaries were calculated for goals, possession, shooting, and disciplinary indicators, together with the distribution of matches across stages.
6. **Exploratory visualisation.** Four multi-panel figures and one team dashboard were produced to examine distributions, stage-level differences, and relationships between variables (see Section 7).
7. **Correlation analysis.** Pearson correlations were calculated for possession vs goals and total attempts vs goals, and a correlation matrix was produced for eight performance metrics.
8. **Team-level aggregation.** Results were aggregated into a 32-team table with matches played, wins, draws, losses, goals scored, goals conceded, goal difference, points, and win rate, then ranked by points.
9. **Summary report.** Key indicators and takeaways were compiled into a statistical summary printed at the end of the notebook.

## 6. Engineered Features

| Feature | Definition |
|---|---|
| `total_goals` | Goals by team 1 plus goals by team 2 |
| `goal_difference` | Absolute difference between the two teams' goals |
| `high_scoring` | True when a match has 3 or more total goals |
| `possession_team1_pct`, `possession_team2_pct` | Possession converted from percentage text to numeric |
| `possession_difference` | Team 1 possession minus team 2 possession |
| `match_outcome` | Winning team, or "Draw" |
| `tournament_stage` | Taken from the `category` field |
| `shooting_accuracy_team1` | On-target attempts divided by total attempts, as a percentage |
| `goal_efficiency_team1` | Goals divided by total attempts, as a percentage |
| `pass_accuracy_team1` | Passes completed divided by passes, as a percentage |
| Team `Points` and `Win Rate (%)` | Team-level aggregates used in the standings table |

## 7. Visual Analysis Performed

| Figure | Panels |
|---|---|
| **Goals and Possession Analysis** | Distribution of total goals per match; goals by tournament stage (box plot); goal-difference distribution; possession vs goals scored with regression line |
| **Possession and Shooting Performance** | Distribution of possession difference; possession by tournament stage; total attempts vs goals; on-target attempts vs goals |
| **Discipline and Match Intensity** | Shooting accuracy distribution; distribution of yellow cards, red cards, and fouls; fouls vs yellow cards; high-scoring matches by stage |
| **Advanced Team Performance** | Correlation heatmap of eight performance metrics; goal efficiency by stage; pass accuracy vs possession; defensive pressure vs forced turnovers |
| **Team Performance Dashboard** | Top 10 teams by points; goals scored vs goals conceded; distribution of team win rates with mean line; goal difference vs points with top teams labelled |

## 8. Key Findings

### Tournament overview

| Indicator | Value |
|---|---|
| Matches analysed | 64 |
| Total goals | 172 |
| Average goals per match | 2.69 |
| Highest-scoring match | 8 goals |
| Matches with 3 or more goals | 30 (46.9%) |
| Most common goal difference | 1 |
| Share of matches with equal goals for both teams | 23.4% |

### Possession and shooting

| Indicator | Value |
|---|---|
| Average possession gap between teams | 18.72 percentage points |
| Correlation: possession vs goals scored | 0.264 (weak positive) |
| Correlation: total attempts vs goals scored | 0.401 (moderate positive) |
| Average shooting accuracy | 37.21% |

Shot volume showed a stronger association with goals than possession did in this dataset.

### Discipline and match intensity

| Indicator | Value per match |
|---|---|
| Yellow cards | 3.53 |
| Red cards | 0.06 |
| Fouls | 25.00 |

### Team performance (top 10 by points)

| Rank | Team | Played | W | D | L | Goals For | Goals Against | Goal Diff. | Points | Win Rate (%) |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | France | 7 | 5 | 1 | 1 | 16 | 8 | +8 | 16 | 71.43 |
| 2 | Argentina | 7 | 4 | 2 | 1 | 15 | 8 | +7 | 14 | 57.14 |
| 3 | Netherlands | 5 | 3 | 2 | 0 | 10 | 4 | +6 | 11 | 60.00 |
| 4 | Morocco | 7 | 3 | 2 | 2 | 6 | 5 | +1 | 11 | 42.86 |
| 5 | England | 5 | 3 | 1 | 1 | 13 | 4 | +9 | 10 | 60.00 |
| 6 | Brazil | 5 | 3 | 1 | 1 | 8 | 3 | +5 | 10 | 60.00 |
| 7 | Croatia | 7 | 2 | 4 | 1 | 8 | 7 | +1 | 10 | 28.57 |
| 8 | Portugal | 5 | 3 | 0 | 2 | 12 | 6 | +6 | 9 | 60.00 |
| 9 | Japan | 4 | 2 | 1 | 1 | 5 | 4 | +1 | 7 | 50.00 |
| 10 | Senegal | 4 | 2 | 0 | 2 | 5 | 7 | -2 | 6 | 50.00 |

Observations drawn from the table:
- The 32-team table spans all participating teams; the highest points total was 16.
- Netherlands recorded no losses across its 5 matches.
- England had the best goal difference (+9) among the top 10, and Croatia recorded the most draws (4) among them.

## 9. Limitations

- The analysis is descriptive and exploratory. No predictive or machine learning models are built.
- Relationship analyses (possession, attempts, fouls, defensive pressure, and similar) use the `team1` columns, so each match contributes one team's perspective rather than both.
- Correlation coefficients describe association only and do not establish causation.
- The sample is a single tournament of 64 matches, so findings should not be generalised to other competitions.
- The dataset is read from a local file path in the notebook; the CSV is not bundled with the exported HTML.

## 10. How to View or Reproduce

**View the results**
1. Download `FiFA2022_ANALYSIS.html`.
2. Open it in any modern web browser.

**Reproduce the analysis**
1. Obtain the match dataset (`Fifa_world_cup_matches.csv`, 64 rows and 88 columns).
2. Install the required libraries:
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
   (`datetime` and `warnings` are part of the Python standard library and need no installation.)
3. Create a notebook with the code from the HTML export and update the file path in the data-loading cell, which currently points to a local Windows directory:
   ```python
   df = pd.read_csv("Fifa_world_cup_matches.csv")
   ```
4. Run the cells in order.

## 11. Professional Relevance

This project demonstrates skills directly applicable to statistics, data analysis, and data science roles:

| Skill area | Evidence in this project |
|---|---|
| Data preparation | Dataset validation, type conversion, and creation of derived metrics from an 88-variable dataset |
| Statistical analysis | Descriptive statistics, distribution analysis, stage-level comparisons, and correlation analysis with interpretation of strength |
| Data visualisation | Structured multi-panel figures, regression overlays, a correlation heatmap, and a dashboard-style summary |
| Aggregation and ranking | Construction of a 32-team standings table from match-level records |
| Analytical communication | Results consolidated into a statistical summary report with stated takeaways and documented limitations |
| Python data stack | Applied use of pandas, NumPy, Matplotlib, and Seaborn |

## 12. Author


**[Jamil Mahida]**
