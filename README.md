# Netflix Data Analysis

An exploratory data analysis (EDA) project on Netflix titles using Python, Pandas, and Matplotlib. The project covers data inspection, missing-value handling, duplicate checking, feature extraction, statistical analysis, and visualization.

## 📌 Project Overview

This project analyzes a Netflix titles dataset containing information about Movies and TV Shows.

The notebook starts with basic dataset inspection and cleaning, then explores:

- Movies vs TV Shows
- Content distribution by country
- Netflix genres/categories
- Content ratings
- Release-year trends
- Year-wise comparison of Movies and TV Shows
- Movie duration
- Number of seasons in TV Shows
- Content added to Netflix by year

The notebook contains **74 cells** and was executed using **Python 3.13.5** with a Python 3 (ipykernel) environment.

## 🎯 Objectives

The main objectives of this analysis are to:

1. Understand the structure of the Netflix dataset.
2. Identify and handle missing values.
3. Check and remove duplicate records.
4. Analyze the distribution of Movies and TV Shows.
5. Find the countries with the highest number of titles.
6. Identify the most frequent Netflix genres/categories.
7. Examine content-rating distribution.
8. Analyze titles by release year.
9. Compare Movies and TV Shows across release years.
10. Analyze movie duration in minutes.
11. Analyze the number of seasons of TV Shows.
12. Examine how many titles were added to Netflix in each year.
13. Save the cleaned dataset for further use.

## 📂 Dataset

The notebook loads the dataset from:

```text
../data/netflix_titles.csv
```

### Dataset dimensions

- **Rows:** 8,807
- **Columns:** 12

### Columns

| Column | Description |
|---|---|
| `show_id` | Unique ID of the title |
| `type` | Movie or TV Show |
| `title` | Title name |
| `director` | Director of the title |
| `cast` | Cast information |
| `country` | Country information |
| `date_added` | Date the title was added to Netflix |
| `release_year` | Original release year |
| `rating` | Content rating |
| `duration` | Movie duration or TV Show seasons |
| `listed_in` | Genre/category information |
| `description` | Title description |

## 🧹 Data Cleaning

The notebook performs the following cleaning steps:

### 1. Dataset inspection

The project checks:

- Dataset shape
- Column names
- Data types
- Non-null counts
- Missing values

Initially, missing values were found in:

- `director`: 2,634
- `cast`: 825
- `country`: 831
- `date_added`: 10
- `rating`: 4
- `duration`: 3

### 2. Duplicate check

Duplicate records were checked using:

```python
df.duplicated().sum()
```

The result was **0 duplicates**.

`drop_duplicates()` was also applied to ensure duplicate rows were removed if present.

### 3. Missing-value handling

Missing values in the following columns were replaced with `"Unknown"`:

```python
['director', 'cast', 'country', 'date_added', 'rating', 'duration']
```

After this step, the notebook converts `date_added` to datetime using:

```python
pd.to_datetime(df['date_added'], errors='coerce')
```

Because `"Unknown"` cannot be converted to a date, those values become `NaT`. The final missing-value check therefore shows **98 missing values in `date_added`**, while the other columns have no missing values.

## 📊 Exploratory Data Analysis

### 1. Movies vs TV Shows

The dataset contains:

| Type | Count | Percentage |
|---|---:|---:|
| Movie | 6,131 | 69.62% |
| TV Show | 2,676 | 30.38% |

Movies form the larger portion of the dataset.

A bar chart is included in the notebook to visualize this distribution.

---

### 2. Top 10 Countries

The notebook calculates the top 10 countries using the `country` column:

| Rank | Country | Titles |
|---:|---|---:|
| 1 | United States | 2,818 |
| 2 | India | 972 |
| 3 | Unknown | 831 |
| 4 | United Kingdom | 419 |
| 5 | Japan | 245 |
| 6 | South Korea | 199 |
| 7 | Canada | 181 |
| 8 | Spain | 145 |
| 9 | France | 124 |
| 10 | Mexico | 110 |

A bar chart is also created for the top 10 countries.

> **Note:** The `Unknown` category is included because missing country values were replaced during cleaning.

---

### 3. Top 10 Genres

For genre analysis, the notebook splits the comma-separated `listed_in` values and expands them into individual genre entries:

```python
genres = df['listed_in'].str.split(', ').explode()
```

The top 10 individual genres/categories are:

| Rank | Genre / Category | Titles |
|---:|---|---:|
| 1 | International Movies | 2,752 |
| 2 | Dramas | 2,427 |
| 3 | Comedies | 1,674 |
| 4 | International TV Shows | 1,351 |
| 5 | Documentaries | 869 |
| 6 | Action & Adventure | 859 |
| 7 | TV Dramas | 763 |
| 8 | Independent Movies | 756 |
| 9 | Children & Family Movies | 641 |
| 10 | Romantic Movies | 616 |

The notebook also contains a separate bar-chart visualization based directly on the raw `listed_in` values, so those chart categories represent the original category combinations rather than the exploded individual genres.

---

### 4. Content Ratings

The rating distribution is analyzed using `value_counts()`.

The five most common ratings are:

| Rank | Rating | Titles |
|---:|---|---:|
| 1 | TV-MA | 3,207 |
| 2 | TV-14 | 2,160 |
| 3 | TV-PG | 863 |
| 4 | R | 799 |
| 5 | PG-13 | 490 |

The notebook also displays the complete rating frequency table and creates a top-10 rating bar chart.

---

### 5. Release Year Analysis

The notebook analyzes the number of titles by `release_year`.

The dataset contains **74 distinct release years**, ranging from **1925 to 2021**.

For recent years, the counts are:

| Release Year | Titles |
|---:|---:|
| 2017 | 1,032 |
| 2018 | 1,147 |
| 2019 | 1,030 |
| 2020 | 953 |
| 2021 | 592 |

A line chart is used to visualize the number of titles across release years.

---

### 6. Movies vs TV Shows by Release Year

The notebook groups titles by both `release_year` and `type` to compare Movies and TV Shows year by year.

The last 10 release years shown in the notebook are:

| Release Year | Movies | TV Shows |
|---:|---:|---:|
| 2012 | 173 | 64 |
| 2013 | 225 | 63 |
| 2014 | 264 | 88 |
| 2015 | 398 | 162 |
| 2016 | 658 | 244 |
| 2017 | 767 | 265 |
| 2018 | 767 | 380 |
| 2019 | 633 | 397 |
| 2020 | 517 | 436 |
| 2021 | 277 | 315 |

A line chart is included for the year-wise comparison.

---

### 7. Movie Duration Analysis

For Movies, the notebook extracts the numeric value from the `duration` column and creates a new feature:

```python
duration_min
```

The movie-duration statistics are:

| Statistic | Value |
|---|---:|
| Count | 6,128 |
| Mean | 99.58 minutes |
| Standard Deviation | 28.29 minutes |
| Minimum | 3 minutes |
| 25th Percentile | 87 minutes |
| Median | 98 minutes |
| 75th Percentile | 114 minutes |
| Maximum | 312 minutes |

A histogram is used to visualize the distribution of movie duration.

---

### 8. TV Show Seasons Analysis

For TV Shows, the notebook extracts the numeric season count from `duration` and creates a new feature:

```python
seasons
```

The five most common season counts are:

| Seasons | TV Shows |
|---:|---:|
| 1 | 1,793 |
| 2 | 425 |
| 3 | 199 |
| 4 | 95 |
| 5 | 65 |

The complete analysis shows season counts ranging from **1 to 17 seasons** in the extracted data.

A bar chart is included to visualize the number of TV Shows by season count.

---

### 9. Content Added to Netflix by Year

The notebook converts `date_added` into datetime format and extracts the year.

The number of titles added by year is:

| Year Added | Titles |
|---:|---:|
| 2008 | 2 |
| 2009 | 2 |
| 2010 | 1 |
| 2011 | 13 |
| 2012 | 3 |
| 2013 | 10 |
| 2014 | 23 |
| 2015 | 73 |
| 2016 | 418 |
| 2017 | 1,164 |
| 2018 | 1,625 |
| 2019 | 1,999 |
| 2020 | 1,878 |
| 2021 | 1,498 |

The highest number of titles added in a single year in this analysis is **1,999 in 2019**.

## 📈 Visualizations Included

The notebook creates visualizations for:

- Movies vs TV Shows
- Top 10 Countries by Netflix Content
- Top 10 Netflix genre/category combinations
- Top 10 Content Ratings
- Netflix Content by Release Year
- Movies vs TV Shows by Release Year
- Distribution of Movie Duration
- Number of Seasons in Netflix TV Shows
- Top 10 individual genres/categories

## 🔍 Key Insights

Based on the executed analysis:

- The dataset contains **8,807 titles** across **12 columns**.
- Movies account for **69.62%** of the dataset, while TV Shows account for **30.38%**.
- The **United States** has the highest number of titles in the country analysis, followed by **India**.
- After splitting multi-category `listed_in` values, **International Movies** is the most frequent individual category, followed by **Dramas** and **Comedies**.
- **TV-MA** is the most common content rating.
- The dataset contains titles released from **1925 through 2021**.
- Among the recent release years shown, **2018** has the highest title count with **1,147**.
- The average movie duration is approximately **99.58 minutes**, with a median of **98 minutes**.
- **1-season TV Shows** are by far the most common season count in the dataset.
- The highest number of titles added to Netflix in a year in this analysis was **1,999 in 2019**.

## 🛠️ Technologies Used

- **Python 3.13.5**
- **Pandas**
- **Matplotlib**
- **Jupyter Notebook**
- **CSV**

## 📁 Project Structure

The notebook expects the dataset in a `data` directory one level above the notebook location:

```text
project/
│
├── data/
│   ├── netflix_titles.csv
│   └── netflix_cleaned.csv
│
└── notebook-folder/
    └── Netflix_Data_Analysis.ipynb
```

If you keep the notebook and `data` folder at the same repository level instead, update the notebook paths from:

```text
../data/netflix_titles.csv
../data/netflix_cleaned.csv
```

to the appropriate repository-relative paths.

## ▶️ How to Run

### 1. Clone the repository

```bash
git clone <your-repository-url>
```

### 2. Open the project in VS Code or Jupyter Notebook

Open:

```text
Netflix_Data_Analysis.ipynb
```

### 3. Install the required libraries

```bash
pip install pandas matplotlib jupyter
```

### 4. Make sure the dataset is available

Place:

```text
netflix_titles.csv
```

inside the expected `data` folder.

### 5. Run the notebook

Execute the cells from top to bottom to reproduce the analysis.

The notebook saves the cleaned dataset as:

```text
../data/netflix_cleaned.csv
```

## 📌 Project Workflow

```text
Load Dataset
     ↓
Inspect Dataset
     ↓
Check Missing Values
     ↓
Check Duplicates
     ↓
Handle Missing Values
     ↓
Exploratory Data Analysis
     ↓
Feature Extraction
     ├── Movie Duration → duration_min
     └── TV Show Seasons → seasons
     ↓
Statistical Analysis
     ↓
Data Visualization
     ↓
Final Dataset Check
     ↓
Save Cleaned Dataset
```

## 📄 Output

The cleaned dataset is exported using:

```python
df.to_csv("../data/netflix_cleaned.csv", index=False)
```

The final dataset retains the original **8,807 rows and 12 columns**. After datetime conversion, the final missing-value check reports **98 missing values in `date_added`** because the original `"Unknown"` entries cannot be converted into valid dates.

## 👨‍💻 Author

**Mohammad Sufiyan**

B.Tech | Computer Science & Engineering
