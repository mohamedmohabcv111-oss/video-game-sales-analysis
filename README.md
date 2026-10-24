# Video Game Sales Analysis & Market Insights

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Plots-4c72b0)](https://seaborn.pydata.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557c)](https://matplotlib.org/)
[![Kaggle](https://img.shields.io/badge/Kaggle-Dataset-20BEFF?logo=kaggle&logoColor=white)](https://www.kaggle.com/datasets/gregorut/videogamesales)

An end-to-end exploratory data analysis (EDA) investigating historical video game sales across global markets, consoles, genres, and publishers. This project uncovers regional buying habits, platform lifecycles, bestseller distributions, and the key drivers of worldwide commercial success.

---

## Table of Contents
- [Overview](#overview)
- [Dataset Description](#dataset-description)
- [Technologies & Libraries Used](#technologies--libraries-used)
- [Data Cleaning & Preprocessing](#data-cleaning--preprocessing)
- [Questions Answered & Analysis](#questions-answered--analysis)
  - [Regional Performance & Extremes (Q1 – Q6)](#1-regional-performance--extremes)
  - [Platform & Genre Market Share (Q7 – Q10)](#2-platform--genre-market-share)
  - [Visual Insights & Strategic Trends (Q11 – Q14)](#3-visual-insights--strategic-trends)
- [Key Insights & Findings](#key-insights--findings)
- [Repository Structure](#repository-structure)
- [Getting Started & Installation](#getting-started--installation)
- [Author & Acknowledgments](#author--acknowledgments)

---

## Overview

The video game industry has evolved from arcade novelties into one of the largest entertainment sectors in the world. This project analyzes over **16,500 video game titles** to answer key commercial and analytical questions:

- What titles defined regional gaming markets in North America, Europe, and Japan?
- Which genres generate the most global revenue, and which deliver the most consistent median returns?
- What platforms achieved the highest commercial success and catalog volume?
- Which geographical region correlates most strongly with worldwide box-office hits?

All findings are documented interactively in [`Video_game_analysis.ipynb`](Video_game_analysis.ipynb).

---

## Dataset Description

The dataset is sourced directly from Kaggle via the `kagglehub` API ([`gregorut/videogamesales`](https://www.kaggle.com/datasets/gregorut/videogamesales)). It records video games with sales greater than 100,000 copies from 1980 through modern consoles.

| Column | Data Type | Description |
| :--- | :--- | :--- |
| **`Rank`** | Integer | Overall sales ranking |
| **`Name`** | String | Name of the video game |
| **`Platform`** | String | Platform of the game release (e.g., PS2, X360, PS3, Wii, DS) |
| **`Year`** | Integer | Year of release (cleaned to `int64`) |
| **`Genre`** | String | Category of the game (Action, Sports, Shooter, Role-Playing, etc.) |
| **`Publisher`** | String | Publishing company (Nintendo, EA, Activision, Sony, etc.) |
| **`NA_Sales`** | Float | Sales in North America (in millions of units) |
| **`EU_Sales`** | Float | Sales in Europe (in millions of units) |
| **`JP_Sales`** | Float | Sales in Japan (in millions of units) |
| **`Other_Sales`** | Float | Sales in the rest of the world (in millions of units) |
| **`Global_Sales`** | Float | Total worldwide sales (in millions of units) |

---

## Technologies & Libraries Used

This project leverages modern Python data science and visualization tooling:

- **[Python](https://www.python.org/)**: Core programming language.
- **[Pandas](https://pandas.pydata.org/)**: 
  - Data ingestion, restructuring, filtering, aggregation, and null-value handling.
  - Multi-column group-bys and summary metric calculations (`.agg()`, `.corrwith()`, `.sort_values()`).
- **[NumPy](https://numpy.org/)**: 
  - Underlying vectorized mathematical computations.
- **[Matplotlib](https://matplotlib.org/)**: 
  - Canvas customization, subplots layout, multi-axis figure generation, label rotations, and line plots.
- **[Seaborn](https://seaborn.pydata.org/)**: 
  - High-level statistical visualization including annotated cross-regional heatmaps, outlier-managed boxplots, and multi-panel scatter grids.
- **[KaggleHub](https://github.com/Kaggle/kagglehub)**: 
  - Direct, authenticated programmatic retrieval of the latest dataset version.

---

## Data Cleaning & Preprocessing

Before exploratory analysis, a thorough data quality audit was executed:

1. **Duplicate Verification**: Checked via `df.duplicated().sum()` to confirm each row is unique.
2. **Missing Value Audit**: Identified missing records primarily in `Year` (271 rows) and `Publisher` (58 rows).
3. **Null Handling**: Dropped incomplete records with `.dropna(subset=['Year'])` and `.dropna(subset=['Publisher'])` to ensure reliable historical and publisher-level aggregations.
4. **Data Type Correction**: Converted `Year` from floating-point representation (`float64`, e.g., `2006.0`) to a clean integer format (`int64`, e.g., `2006`) to allow proper chronological grouping.

---

## Questions Answered & Analysis

The analysis is organized into three analytical tracks covering **14 structured questions**:

### 1. Regional Performance & Extremes

* **Question 1: What are the lowest-selling video games in North America (NA)?**
  - Identifies niche and localized games with minimal or zero recorded sales in the North American market.
* **Question 2: What are the top 6 best-selling video games in North America (NA)?**
  - Highlights historic blockbusters in NA, led by Nintendo powerhouses (*Wii Sports*, *Super Mario Bros.*, *Duck Hunt*).
* **Question 3: What are the lowest-selling video games in Europe (EU)?**
  - Isolates regional titles that failed to penetrate European retail markets.
* **Question 4: What are the top 6 best-selling video games in Europe (EU)?**
  - Details Europe’s highest-grossing games, featuring major sports, racing, and accessible party titles.
* **Question 5: What are the lowest-selling video games in Japan (JP)?**
  - Shows titles with zero or negligible Japanese traction, especially western-centric action or sports games.
* **Question 6: What are the top 6 best-selling video games in Japan (JP)?**
  - Demonstrates Japan's distinct preference for RPGs and handheld titles, led by *Pokemon Red/Green/Blue* and classic Mario games.

---

### 2. Platform & Genre Market Share

* **Question 7: Which video game genres generate the highest total global sales?**
  - Aggregates worldwide revenue across genres. **Action** and **Sports** rank as the two highest-grossing genres overall.
* **Question 8: Which gaming platforms have generated the highest total global sales?**
  - Summarizes lifetime sales by console. Heavyweights include the **PlayStation 2 (PS2)**, **Xbox 360 (X360)**, **PlayStation 3 (PS3)**, **Nintendo Wii**, and **Nintendo DS**.
* **Question 9: Which platform has the most games and which sold the most?**
  - Contrasts catalog size (number of published titles) against commercial output (total sales in millions) to reveal platform efficiency and developer adoption.
* **Question 10: What are the 10 best-selling games ever?**
  - Groups global sales across all platform editions to determine the top 10 single most commercially successful video game titles of all time.

---

### 3. Visual Insights & Strategic Trends

* **Question 11: How are video game sales distributed across different genres and regions?**
  - **Visualization**: Annotated Heatmap (`sns.heatmap`)
  - **Insight**: Displays regional revenue matrices, exposing how North America and Europe favor Action, Sports, and Shooters, whereas Japan exhibits outsized demand for Role-Playing games.

* **Question 12: What is the distribution of global sales across different genres?**
  - **Visualization**: Categorical Boxplot (`sns.boxplot`)
  - **Insight**: Highlights median sales performance and interquartile ranges across genres, demonstrating that while Action has massive cumulative volume, certain genres offer higher baseline median sales per title.

* **Question 13: How did total global sales change from year to year, from the earliest year in the data up to 2010?**
  - **Visualization**: Time Series Line Plot with Data Markers (`.plot(kind='line')`)
  - **Insight**: Illustrates the meteoric rise of the gaming industry through the 1990s and 2000s, reaching its peak golden era between 2006 and 2009.

* **Question 14: Which region drives global sales most?**
  - **Visualization**: 2x2 Scatter Plot Matrix & Correlation Analysis (`.corrwith()`, `sns.scatterplot`)
  - **Insight**: Statistically proves that **North America (NA)** has the highest positive correlation with global sales, followed closely by **Europe (EU)**, cementing them as the primary drivers of commercial blockbuster success.

---

## Key Insights & Findings

1. **North America is the Primary Revenue Engine**: NA sales have the strongest mathematical correlation with global sales; games that underperform in NA rarely reach the global top 10.
2. **Japan's Distinct Market Identity**: While NA and EU share similar tastes (Action, Shooters, Sports), the Japanese market is uniquely dominated by **Role-Playing Games (RPGs)** and handheld platforms (Nintendo DS, Game Boy).
3. **Console Dominance**: The **PS2, Xbox 360, PS3, and Wii** represent the pinnacle era of console gaming revenue, combining expansive software libraries with high software tie ratios.
4. **Nintendo's Evergreen Franchises**: Pack-in titles and first-party franchises (*Wii Sports*, *Mario Kart*, *Pokemon*, *Super Mario*) dominate the top slots across global records.

---

## Repository Structure

```plaintext
video-game-sales-analysis/
│
├── Video_game_analysis.ipynb   # Complete analysis notebook with code, markdown & plots
├── requirements.txt            # Python dependencies and versions
├── .gitignore                  # Git ignore rules (virtual environments, caches, checkpoints)
└── README.md                   # Project documentation and summary report
```

---

## Getting Started & Installation

### Prerequisites
- Python 3.10 or higher
- Git

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/mohamedmohabcv111-oss/video-game-sales-analysis.git
   cd video-game-sales-analysis
   ```

2. **Create and activate a virtual environment**:
   ```bash
   # Windows (PowerShell)
   python -m venv .venv
   .venv\Scripts\Activate.ps1

   # macOS / Linux
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Launch Jupyter Notebook**:
   ```bash
   jupyter notebook Video_game_analysis.ipynb
   ```

---

## Author & Acknowledgments

- **Author**: Mohamed Mohab ([@mohamedmohabcv111-oss](https://github.com/mohamedmohabcv111-oss))
- **Dataset**: Provided by Gregory Smith ([gregorut](https://www.kaggle.com/gregorut)) on Kaggle.
- **Analysis Environment**: Built with Jupyter, Python, and the Antigravity IDE.
