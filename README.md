# CodeAlpha Data Analytics Internship — All 4 Tasks

This repo completes **all four** Data Analytics tasks from the CodeAlpha internship
brief. (Instructions only require 2–3, but all four are included here — pick
whichever set you need for your submission form / GitHub repo.)

Each task uses a **real public dataset** and produces **real output** (scraped
data, statistical results, charts, scored review data) — nothing here is
simulated.

```
CodeAlpha_DataAnalytics/
├── Task1_WebScraping/
│   └── web_scraping.py            # scrapes github.com/trending live
├── Task2_EDA/
│   └── eda_titanic.py             # EDA on the Titanic dataset
├── Task3_DataVisualization/
│   └── data_visualization.py      # dashboard + insight chart
├── Task4_SentimentAnalysis/
│   └── sentiment_analysis.py      # VADER sentiment on Amazon reviews
├── data/                          # input datasets + generated summaries
├── outputs/                       # generated charts + scored CSVs
├── requirements.txt
└── README.md
```

## Task 1 — Web Scraping
**Script:** `Task1_WebScraping/web_scraping.py`
Scrapes the **live** GitHub Trending page (`github.com/trending`) with
`requests` + `BeautifulSoup`, extracting repo name, description, language,
total stars/forks, and "stars today" into `data/github_trending_scraped.csv`.

> Note: this page changes daily, so re-running the script gives fresh data —
> that's expected and is a good thing to mention in your project writeup.

## Task 2 — Exploratory Data Analysis (EDA)
**Script:** `Task2_EDA/eda_titanic.py`
**Dataset:** Titanic passenger list — the classic Kaggle "Titanic - Machine
Learning from Disaster" dataset (891 passengers), loaded from
`data/titanic.csv`.

Covers:
- Structure/dtype overview, missing-value & duplicate audit
- 5 meaningful analytical questions (survival by class, sex, embarkation port, family size)
- 3 formal hypothesis tests (chi-square for categorical association, Welch's
  t-test for age difference) with p-values and conclusions
- Saves a grouped summary table to `data/titanic_eda_summary.csv`

Key finding: sex (chi²=260.7, p≈1.2e-58) and passenger class (chi²=102.9,
p≈4.6e-23) are both very strongly associated with survival.

## Task 3 — Data Visualization
**Script:** `Task3_DataVisualization/data_visualization.py`
**Dataset:** same Titanic data as Task 2.

Produces:
- `outputs/titanic_dashboard.png` — 6-panel dashboard (survival counts,
  survival rate by class/sex, age distribution, fare by class, survival vs.
  family size)
- `outputs/survival_by_class_sex.png` — a single presentation-ready chart
  for the strongest insight (class × sex × survival rate)

## Task 4 — Sentiment Analysis
**Script:** `Task4_SentimentAnalysis/sentiment_analysis.py`
**Dataset:** "Consumer Reviews of Amazon Products" (Datafiniti / Kaggle
dataset, ~34,600 real reviews), loaded from `data/amazon_reviews.csv`.

Uses **VADER** (a lexicon + rule-based sentiment tool tuned for short,
informal text like reviews and social media — ships its lexicon inside the
pip package, no extra downloads needed) to classify a 5,000-review sample as
positive/negative/neutral, then checks that against the reviewer's star
rating as a sanity check (**87.6% agreement**).

Outputs:
- `outputs/sentiment_analysis_results.png` — sentiment distribution + VADER
  score vs. star rating boxplot
- `outputs/amazon_reviews_sentiment_scored.csv` — every sampled review with
  its sentiment score and label attached

## How to run

```bash
pip install -r requirements.txt

cd Task1_WebScraping        && python3 web_scraping.py
cd ../Task2_EDA              && python3 eda_titanic.py
cd ../Task3_DataVisualization && python3 data_visualization.py
cd ../Task4_SentimentAnalysis && python3 sentiment_analysis.py
```

## Swapping in your own Kaggle dataset

The scripts are written so the **only thing you need to change is the file
path** if you want to use a different Kaggle dataset for Tasks 2–4:

1. Download your dataset from Kaggle (`kaggle datasets download -d <dataset>`
   or via the website) into the `data/` folder.
2. Update the `DATA_PATH` variable at the top of the relevant script.
3. Update the column names referenced in the script (e.g. `Survived`,
   `reviews.text`) to match your dataset's actual columns.

## Submitting to CodeAlpha

Per the task brief:
1. Push this folder to a GitHub repo named `CodeAlpha_DataAnalytics`.
2. Record a short video walking through your code + results, post it on
   LinkedIn tagging **@CodeAlpha**, and include the GitHub link.
3. Submit through the Submission Form shared in your WhatsApp group.
