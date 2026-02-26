# What-Makes-a-YouTube-Video-Stay-Trending
data science project
🎯 What Makes a YouTube Video Stay Trending?
📌 Project Type

Machine Learning + NLP + Behavioral Data Analysis

1️⃣ Problem Statement

YouTube’s trending page is highly competitive and algorithm-driven.
While many videos gain large numbers of views quickly, only a subset remain trending for multiple consecutive days.

The Core Question:

What differentiates videos that briefly appear on the trending page from those that stay trending for more than 3 days?

We framed the problem as a binary classification task:

stays_long = 1  if trend_days > 3  
stays_long = 0  otherwise
2️⃣ Business Context

Understanding trending longevity helps:

Content creators optimize engagement strategies

Agencies improve title and publishing strategy

Marketers identify sustainable content patterns

Platforms understand reinforcement dynamics

Trending persistence is not about popularity alone — it reflects algorithmic reinforcement driven by user behavior.

3️⃣ Dataset Overview

The dataset combines trending video records across multiple countries, including:

US

GB

DE

CA

FR

IN

JP

KR

MX

RU

Each record includes:

Video metadata (title, description, tags)

Engagement metrics (views, likes, dislikes, comment_count)

Publishing time

Category ID

Country

After merging and cleaning:

~375,000 records

17 original columns

Engineered behavioral and NLP features

4️⃣ Data Challenges & How We Solved Them
🔹 Duplicate Video Entries

Videos appear multiple times across trending dates.

✅ Solution:
We grouped by video_id and calculated unique trend_days.

🔹 Text Noise

Titles and descriptions contain:

URLs

punctuation

emojis

mixed casing

✅ Solution:

Lowercasing

Regex cleaning

Removing special characters

TF-IDF vectorization

🔹 Engagement Bias

Raw views are highly skewed.

✅ Solution:
Instead of relying on raw counts, we engineered:

engagement_ratio = (likes + comments) / views

like_ratio

comment_ratio

This normalized engagement intensity.

🔹 Country Leakage Risk

When testing cross-country generalization, using country_encoded would leak region info.

✅ Solution:
Removed country feature in cross-country experiment.

5️⃣ Feature Engineering

We engineered features across three dimensions:

📊 Behavioral Features

Engagement ratios

Likes per view

Comments per view

These capture interaction density, not popularity.

⏰ Temporal Features

Publish hour

Publish weekday

Captures timing influence on early momentum.

🧠 NLP Features

We incorporated two NLP layers:

1️⃣ Sentiment Analysis

Using VADER:

title_sentiment

description_sentiment

Captures emotional framing.

2️⃣ TF-IDF

Applied on cleaned titles:

500 most important textual features

Captures keyword-level signals.

6️⃣ Modeling Approach

We used:

🌲 Random Forest Classifier

Why Random Forest?

Handles mixed numeric + sparse text features

Robust to outliers

Captures non-linear interactions

Provides feature importance

Training Strategy

1️⃣ Global Model

Random Train/Test split

Stratified by target

2️⃣ Cross-Country Robustness Test

Train on US

Test on GB

This simulates real-world deployment across regions.

7️⃣ Model Evaluation

We evaluated using:

Accuracy

Precision

Recall

F1-score

ROC-AUC

We also visualized:

Confusion Matrix (Plotly)

Feature Importance

Trend duration distributions

8️⃣ Key Findings
🔥 1. Engagement > Views

Raw views were not the strongest predictor.

Instead:

Engagement intensity (likes + comments relative to views) was the most important signal.

This suggests algorithm reinforcement prioritizes interaction density.

💬 2. Textual Framing Matters

Titles with positive sentiment slightly improved longevity.

Certain keywords correlate with sustained trending.

This confirms that framing strategy impacts retention.

🌍 3. Cross-Country Generalization

The model trained on US data maintained reasonable predictive power on GB.

This indicates:

Engagement-based signals are more universal than region-specific behavior.

⏰ 4. Timing Has Secondary Influence

Publishing time showed minor but consistent influence.

Momentum timing affects initial algorithm boost.

9️⃣ What We Learned About the Algorithm

Although YouTube’s algorithm is proprietary, the data suggests:

Reinforcement loops are engagement-driven

Sustained interaction matters more than initial exposure

Content longevity reflects behavioral stickiness

🔟 Limitations

No watch-time or retention data

No thumbnail image features

No comment text analysis

Random Forest only (no boosting models tested)

🔮 Future Improvements

XGBoost comparison

SHAP interpretability

Thumbnail image analysis (Computer Vision)

Time-series modeling of first 24 hours

Deep NLP (transformers on description/comments)

🏁 Final Takeaway

Sustained trending is driven more by engagement intensity than by raw popularity.

Algorithmic reinforcement appears to reward interaction density and emotional framing rather than exposure alone.

🧠 Data Science Highlights

✔ Behavioral feature engineering
✔ Text vectorization + sentiment analysis
✔ Sparse + dense feature integration
✔ Cross-domain robustness testing
✔ Interactive visualization with Plotly
✔ Business-aligned modeling
