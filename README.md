# 🗳️ Political Sentiment Analysis — Canadian Federal Election 2025
### Pierre Poilievre (Conservative) vs Justin Trudeau (Liberal)

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![VADER](https://img.shields.io/badge/NLP-VADER%20Sentiment-red)
![Brand24](https://img.shields.io/badge/Tool-Brand24-blueviolet)
![Octoparse](https://img.shields.io/badge/Tool-Octoparse-orange)
![Social Searcher](https://img.shields.io/badge/Tool-Social%20Searcher-teal)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

> **A multi-platform, multi-tool NLP sentiment analysis of public opinion toward Canada's two leading political figures across Twitter, Facebook, Reddit, YouTube, and niche platforms — revealing the digital narrative battle ahead of the 2025 federal election.**

---

## 📌 Problem Statement

In modern politics, public opinion is increasingly shaped — and expressed — through social media. Understanding **sentiment trends** across platforms provides campaign teams, media analysts, and political strategists with real-time insight into voter concerns, perceptions, and opportunities.

This project conducts a comprehensive sentiment analysis of **Pierre Poilievre (Conservative Party)** and **Justin Trudeau (Liberal Party)** using data from multiple social media platforms. The analysis examines:
- How is each leader perceived across different platforms?
- What events and topics drive positive, neutral, or negative sentiment?
- How do engagement metrics (likes, shares, reposts) amplify specific sentiments?
- What strategic communication adjustments can improve each leader's digital presence?

---

## 🎯 Objectives

| # | Objective |
|---|-----------|
| 1 | Analyze sentiment distribution (positive/neutral/negative) for both parties across platforms |
| 2 | Apply engagement-weighted sentiment scoring to reflect true public amplification |
| 3 | Identify key events and topics driving sentiment spikes |
| 4 | Conduct a comparative sentiment analysis between Poilievre and Trudeau |
| 5 | Deliver platform-specific strategic recommendations |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                      DATA COLLECTION LAYER                          │
│                                                                     │
│   Octoparse          Brand24             Social Searcher            │
│   (Twitter scraping) (Facebook/Twitter   (YouTube, Reddit,          │
│                       monitoring)         Instagram, CBC, niche)    │
│         │                  │                      │                 │
│         └──────────────────┴──────────────────────┘                │
│                            │                                        │
│                            ▼                                        │
│                    DATA PREPROCESSING                               │
│           ├── Remove nulls & duplicates                             │
│           ├── Text cleaning (URLs, hashtags, punctuation)           │
│           ├── Language detection                                    │
│           └── Translation (French → English via Google Translate)   │
│                            │                                        │
│                            ▼                                        │
│                   SENTIMENT SCORING ENGINE                          │
│           ├── VADER Sentiment Analysis (English)                    │
│           ├── TextBlob (multilingual support)                       │
│           └── Weighted Sentiment = Score × (Likes + Replies + Reposts)│
│                            │                                        │
│                            ▼                                        │
│              CLASSIFICATION: Positive / Neutral / Negative          │
│              (Thresholds: >0.05 | -0.05 to 0.05 | <-0.05)         │
│                            │                                        │
│                            ▼                                        │
│             ANALYSIS: Distribution | Events | Comparative           │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 💡 Solution Approach

### Tools Used

| Tool | Platform Coverage | Purpose |
|------|------------------|---------|
| **Octoparse** | Twitter | Web scraping for tweet data (text, likes, replies, reposts) |
| **Brand24** | Twitter + Facebook | Social listening, brand monitoring, real-time sentiment tracking |
| **Social Searcher** | YouTube, Reddit, Instagram, CBC, niche forums | Multi-platform sentiment monitoring |

### Methodology

#### Step 1 — Data Preprocessing
- Removed rows with missing text fields
- Eliminated duplicate tweets/posts to prevent sentiment bias
- Cleaned text: removed URLs, @mentions, #hashtags, punctuation, numbers
- Standardized all text to lowercase
- Detected tweet language and translated **French tweets → English** using Google Translate API

#### Step 2 — Sentiment Scoring
- **VADER (Valence Aware Dictionary and sEntiment Reasoner)**: Primary scorer for English text — highly optimized for social media language
- **TextBlob**: Secondary scorer for multilingual content
- Combined both scores to enhance accuracy

#### Step 3 — Classification Thresholds
```
Positive  :  Compound Score > 0.05
Neutral   : -0.05 ≤ Compound Score ≤ 0.05
Negative  :  Compound Score < -0.05
```

#### Step 4 — Engagement-Weighted Sentiment
```
Weighted Sentiment = Sentiment Score × (Likes + Replies + Reposts)
```
This approach ensures that highly engaging posts (viral content) carry proportionally more weight in the final sentiment picture.

---

## 📊 Results & Key Findings

### 🐦 Octoparse — Twitter Sentiment (Party Level)

| Party | Positive | Neutral | Negative | Weighted Score |
|-------|----------|---------|----------|----------------|
| **Liberal Party** | 400 tweets | 150 tweets | 250 tweets | **+800** |
| **Conservative Party** | 350 tweets | 100 tweets | 400 tweets | **-400** |

- Liberal Party's positive tweets attract **higher engagement** (likes/reposts), amplifying their weighted score
- Conservative Party's negative tweets dominate interactions, dragging their weighted sentiment to -400

---

### 📊 Brand24 — Facebook & Twitter (Poilievre, 3-Month Period)

| Sentiment | Mentions | Percentage |
|-----------|----------|------------|
| Positive | 128 | 3.88% |
| **Negative** | **729** | **21.37%** |
| Neutral | ~2,460 | 74.75% |

**Top Topics Driving Sentiment:**

| Topic | Mentions | Reach | Dominant Sentiment |
|-------|----------|-------|-------------------|
| Trudeau-Poilievre Dynamics | 1,400 | 31M | Mixed (slight negative) |
| Canadian Economic Policies | 461 | 5.9M | Neutral/moderate negative |
| Canadian Religious Tensions | 89 | 877K | Mostly negative |
| Hindu Temple Attack | 48 | 469K | Strongly negative |

---

### 🌐 Social Searcher — Multi-Platform (Poilievre)

| Sentiment | Posts | Percentage |
|-----------|-------|------------|
| **Positive** | 52 | **16%** |
| Negative | 34 | 10% |
| Neutral | 240 | 74% |
| **Positive-to-Negative Ratio** | | **3:2** |

**Positive drivers:** Carbon tax repeal policies, fiscal responsibility platform, leadership as Trudeau alternative

**Negative drivers:** Trump comparisons, divisive rhetoric perception, policy feasibility skepticism

---

### ⚖️ Comparative Analysis — Poilievre vs Trudeau

| Metric | Poilievre | Trudeau |
|--------|-----------|---------|
| Total Mentions | 3,400 | **17,000** |
| Positive Sentiment | 4% (130 mentions) | 4% (588 mentions) |
| **Negative Sentiment** | **22%** (732 mentions) | 14% (2,239 mentions) |
| Social Media Mentions | 1,650 | **5,800** |

> 📌 While Trudeau receives proportionally **lower negative sentiment (14% vs 22%)**, Poilievre has a stronger engagement intensity per mention — suggesting a more vocal but polarized base.

---

### 🔑 Keyword & Hashtag Analysis

**Most Frequent Hashtags:**
- `#canada` (408 mentions) — national conversations dominate
- `#pierrepoilievre` (379 mentions) — high direct engagement
- `#justintrudeau` (333 mentions)
- `#cdnpoli` — Canadian political discussions
- `#politics` (105 mentions)

**Bag of Words Highlights:** `leader`, `conservative`, `Canada`, `Trudeau`, `minister`, `tax`, `election` — confirming economic policy and leadership rivalry as the central discourse themes

---

## 🛠️ Tech Stack

| Tool / Library | Purpose |
|---------------|---------|
| **Python 3.x** | Core scripting and analysis |
| **VADER (NLTK)** | Social media-optimized sentiment scoring |
| **TextBlob** | Multilingual sentiment support |
| **Google Translate API** | French → English translation |
| **Pandas** | Data manipulation and aggregation |
| **Octoparse** | Twitter data scraping |
| **Brand24** | Social listening and monitoring |
| **Social Searcher** | Multi-platform content tracking |
| **Matplotlib / Seaborn** | Visualization of sentiment distributions |

---

## 📁 Project Structure

```
political-sentiment-analysis/
│
├── data/
│   ├── liberal_tweets.csv               # Octoparse Twitter data — Liberal Party
│   ├── conservative_tweets.csv          # Octoparse Twitter data — Conservative Party
│   ├── brand24_poilievre.csv           # Brand24 export — Poilievre mentions
│   └── social_searcher_export.csv       # Social Searcher multi-platform data
│
├── notebooks/
│   └── sentiment_analysis.ipynb         # Full NLP pipeline: cleaning → scoring → viz
│
├── visuals/
│   ├── liberal_sentiment_dist.png       # Pie/bar chart — Liberal sentiment
│   ├── conservative_sentiment_dist.png  # Pie/bar chart — Conservative sentiment
│   ├── weighted_sentiment_comparison.png
│   ├── topic_sentiment_breakdown.png    # Brand24 topic analysis
│   ├── poilievre_vs_trudeau.png        # Comparative bar chart
│   ├── keyword_cloud.png               # Bag of words visualization
│   └── hashtag_frequency.png
│
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas nltk textblob googletrans==4.0.0rc1 matplotlib seaborn
python -m nltk.downloader vader_lexicon
```

### Run the Analysis
```bash
git clone https://github.com/yourusername/political-sentiment-analysis.git
cd political-sentiment-analysis
jupyter notebook notebooks/sentiment_analysis.ipynb
```

### Core Code Snippet
```python
from nltk.sentiment.vader import SentimentIntensityAnalyzer
import pandas as pd

sia = SentimentIntensityAnalyzer()

def classify_sentiment(text):
    score = sia.polarity_scores(text)['compound']
    if score > 0.05:
        return 'Positive'
    elif score < -0.05:
        return 'Negative'
    else:
        return 'Neutral'

df['sentiment'] = df['cleaned_text'].apply(classify_sentiment)

# Weighted sentiment
df['weighted_sentiment'] = (
    df['vader_score'] * (df['likes'] + df['replies'] + df['reposts'])
)
```

---

## 📋 Strategic Recommendations

### For Pierre Poilievre (Conservative Party)
| Area | Recommendation |
|------|---------------|
| **Policy Messaging** | Deliver clearer, actionable plans — address undecided neutral voters (74%) |
| **Controversial Topics** | Directly address Trump comparisons and immigration criticism with transparency |
| **Platform Strategy** | Invest heavily in YouTube (positive sentiment stronger); manage Twitter narratives proactively |
| **Neutral Conversion** | Town halls, Q&A sessions, and detailed policy infographics to convert the 74% neutral base |

---

## ⚠️ Limitations

- Sentiment analysis tools (VADER, TextBlob) may misclassify **sarcasm, irony, or culturally nuanced language**
- **Sampling bias** — Brand24 and Social Searcher are not exhaustive; data collection windows may miss key events
- Translation quality may introduce noise for **French-language tweets** from Québec
- Media outlet framing (CBC, CTV) influences neutral sentiment classification — editorial tone is not captured
- Sentiment doesn't equal **voting intention** — high negative sentiment can still reflect high engagement and awareness

---

## 🌍 Project Impact

| Stakeholder | Benefit |
|-------------|---------|
| **Campaign Teams** | Real-time intelligence for message refinement and crisis response |
| **Media Analysts** | Quantified evidence of narrative framing across platforms |
| **Political Strategists** | Segment-specific insights (supporters, critics, undecided) |
| **Researchers** | Framework for replicable cross-platform political NLP analysis |

---

## 📚 References

- Hutto, C.J. & Gilbert, E.E. (2014). *VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text.*
- Brand24: https://brand24.com
- Octoparse: https://www.octoparse.com
- Social Searcher: https://www.social-searcher.com
- NLTK VADER: https://www.nltk.org/howto/sentiment.html

---

## 👤 Author

**[Mahima Srinivasan]**
- 📧 [mahima.s3994@gmail.com]
- 💼 [linkedin.com/in/mahimasrinivasan3994]

> *This project demonstrates NLP-based text analytics, multi-tool social media data collection, engagement-weighted sentiment modeling, and the translation of public opinion data into strategic communication insights.*

---

*⭐ If you found this project insightful, please consider starring the repository!*
