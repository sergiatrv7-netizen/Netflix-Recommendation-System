# Netflix-Recommendation-System
Hybrid recommendation system using collaborative filtering, content-based filtering, and business rules.


# 🎬 Netflix Recommendation System — Hybrid Recommendation Engine

> A hybrid content recommendation system developed in Python using user behavior, catalog information, collaborative filtering, content-based filtering, and business rules.

---

## 📌 Project Overview

This project consists of the development of a **hybrid recommendation system inspired by a streaming platform such as Netflix**.

The main objective is to analyze user behavior and generate personalized movie and TV show recommendations based on users' viewing history and content preferences.

The recommendation engine combines three main approaches:

* **Item-Based Collaborative Filtering**
* **Content-Based Filtering using TF-IDF**
* **Business Rules**

These components are combined through a **linear blender** that generates a final recommendation score used to rank content for each user.

The project also includes a complete data science workflow:

**Data Exploration → Data Cleaning → Analysis → Modeling → Evaluation → Explainability**

---

# 🎯 Objectives

## General Objective

Develop a hybrid recommendation system capable of generating personalized content recommendations using user viewing history and catalog information.

## Specific Objectives

* Analyze the quality of the available datasets.
* Detect and document data anomalies.
* Clean and prepare the data for modeling.
* Analyze user behavior and consumption patterns.
* Analyze the available content catalog.
* Build a user-item interaction matrix.
* Implement item-based collaborative filtering.
* Implement content-based filtering using TF-IDF.
* Incorporate business rules into the recommendation process.
* Address the cold-start problem.
* Evaluate the recommendation system using ranking metrics.
* Analyze model limitations.
* Implement recommendation explainability.

---

# 🗂️ Project Structure

```text
Netflix-Recommendation-System/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── README.md
│   └── processed/
│       └── viewing_history_clean.csv
│
├── notebooks/
│   └── ProyectoFinalFINALISIMO.ipynb
│
└── reports/
    └── figures/
        ├── eda/
        ├── users/
        ├── catalog/
        └── evaluation/
```

### Folder Description

| Folder/File        | Description                                     |
| ------------------ | ----------------------------------------------- |
| `data/`            | Dataset documentation and processed data        |
| `data/processed/`  | Cleaned datasets used by the project            |
| `notebooks/`       | Main analysis and modeling notebook             |
| `reports/figures/` | Generated visualizations and evaluation plots   |
| `README.md`        | Project documentation                           |
| `requirements.txt` | Python dependencies                             |
| `.gitignore`       | Files and folders excluded from version control |

---

# 📊 Datasets

The project is based on three main sources of information.

## 1. User Dataset

**`netflix_users_data.csv`**

Contains information related to platform users, including variables such as:

* `user_id`
* Age
* Country
* Subscription type
* Viewing hours
* User status
* Device

---

## 2. Content Catalog

**`NetFlix_catalog.csv`**

Contains information about the available movies and TV shows:

* `show_id`
* Title
* Content type
* Director
* Cast
* Country
* Date added
* Release year
* Rating
* Duration
* Genres
* Availability

---

## 3. Viewing History

**`viewing_history.csv`**

Contains user-content interaction records such as:

* `user_id`
* `show_id`
* Viewing date
* Viewing duration
* Percentage watched
* Rating
* Completion status
* Additional interaction information

The dataset contains intentionally inconsistent records, making data quality analysis and cleaning an important part of the project.

---

# 🧹 1. Exploratory Data Analysis

The first stage of the project consists of exploring the available datasets.

The analysis includes:

* Data types.
* Missing values.
* Duplicate records.
* Out-of-range values.
* Invalid IDs.
* Inconsistent relationships between datasets.
* Invalid dates.
* Negative values.
* Inconsistent durations.
* Logical inconsistencies between variables.

### Examples of Data Anomalies

The project identifies and handles issues such as:

* Ratings outside the expected range.
* Viewing percentages above 100%.
* Negative or zero viewing durations.
* Viewing durations longer than the actual content duration.
* Users or content IDs that do not exist.
* Duplicate records.
* Contradictory duplicate interactions.
* Invalid or future dates.
* Inconsistencies between completion status and percentage watched.
* Missing values in critical columns.

The cleaning process documents which records were removed, modified, or retained and the reason for each decision.

---

# 📈 2. Exploratory Analysis and Visualization

Several visualizations are used to identify relevant patterns in the data.

The analysis includes:

* Rating distributions.
* User distributions.
* Viewing behavior by age.
* Viewing behavior by country.
* Viewing trends over time.
* Most watched content.
* Movies vs. TV shows.
* Most frequent genres.
* Most frequent directors and actors.
* Active vs. inactive users.
* Device usage patterns.

Interactive visualizations were also developed using **Plotly**.

---

# 👥 3. User Profiling

User behavior is analyzed using both demographic and behavioral characteristics.

The analysis considers:

* Age.
* Country.
* Subscription type.
* Viewing hours.
* Preferred genres.
* Average rating.
* Device.
* User status.

**K-Means clustering** is also used to explore groups of users with similar consumption patterns.

This allows the project to identify potential user profiles and differences between active and inactive users.

---

# 🎞️ 4. Catalog Analysis

The content catalog is analyzed to understand its composition and relationship with user consumption.

The analysis includes:

* Movies vs. TV shows.
* Content distribution by country.
* Release-year distribution.
* Most frequent genres.
* Most frequent directors.
* Most frequent actors.
* Content availability.
* Relationship between content availability and consumption.

---

# 🤖 5. Hybrid Recommendation System

The main component of the project is a hybrid recommendation engine combining three different sources of information.

## 5.1 Item-Based Collaborative Filtering

A user-item matrix is constructed:

```text
              Show A   Show B   Show C   Show D
User 1           5        4        -        3
User 2           4        -        5        4
User 3           -        5        4        -
```

The matrix represents the relationship between users and content through their ratings.

Ratings are normalized and **cosine similarity between items** is calculated.

For content that a user has not watched yet, the system estimates its rating using content similar to the items the user has already consumed.

The prediction is calculated through a similarity-weighted average.

---

# 🎯 5.2 Content-Based Filtering

The second component uses the characteristics of the content itself.

Content genres are transformed into numerical representations using:

**TF-IDF — Term Frequency / Inverse Document Frequency**

A user preference profile is then constructed using content that the user has rated positively.

The similarity between the user profile and each content item is calculated using cosine similarity.

This component also provides an alternative strategy for users with limited interaction history.

---

# ⚙️ 5.3 Business Rules

The third component incorporates contextual information and business-oriented rules.

These include:

* Popularity within the user's country.
* Preference for content type.
* Content freshness.
* Exclusion of already watched titles.
* Exclusion of unavailable content.

Business rules allow the recommendation engine to incorporate domain knowledge that cannot necessarily be learned directly from ratings.

---

# ⚖️ 6. Hybrid Blender

The three components are combined through a linear scoring function:

```text
score_total =
    α · score_cf
    + β · score_cb
    + γ · score_rules
```

Where:

| Component     | Description                    |
| ------------- | ------------------------------ |
| `score_cf`    | Collaborative filtering score  |
| `score_cb`    | Content-based similarity score |
| `score_rules` | Business rule score            |
| `α`           | Collaborative filtering weight |
| `β`           | Content-based weight           |
| `γ`           | Business rules weight          |

The weights were calibrated using temporal validation.

The best-performing combination was:

```text
α = 0.1
β = 0.8
γ = 0.1
```

This indicates that the **Content-Based component contributes the most to the final ranking** for this dataset.

---

# 🎬 7. Recommendation Function

The main recommendation function is:

```python
recomendar(user_id, n=10, min_rating=3)
```

It receives:

* `user_id`: User identifier.
* `n`: Number of recommendations.
* `min_rating`: Minimum rating used to construct user preferences.

The function returns recommendation information such as:

* Content ID.
* Title.
* Content type.
* Genres.
* Description.
* Duration.
* Cast.
* Director.
* Estimated rating.
* Final recommendation score.
* Recommendation explanation.

Example:

```python
{
    "show_id": "s1234",
    "title": "Example Movie",
    "type": "Movie",
    "genres": "Drama",
    "score": 0.92,
    "explanation": "Recommended based on the similarity between the user's content profile and the genres of this title."
}
```

---

# 🧊 8. Cold-Start Strategy

One of the main challenges in recommendation systems is the **cold-start problem**.

This occurs when a user has very little historical information available.

For users with sufficient history:

```text
User History
     ↓
Hybrid Recommendation System
     ↓
Collaborative Filtering
+ Content-Based Filtering
+ Business Rules
```

For users with insufficient history:

```text
Limited History
     ↓
Content-Based Filtering
```

This allows the system to generate recommendations even when collaborative filtering does not have enough information.

---

# 🧪 9. Model Evaluation

To reduce the risk of **data leakage**, the project uses a temporal evaluation strategy.

### Training Period

```text
2023-01-01 → 2024-12-31
```

### Test Period

```text
2025-01-01 → 2025-12-31
```

A content item is considered relevant when the user actually watched it during 2025 and gave it a rating equal to or above the defined threshold.

---

# 📏 10. Evaluation Metrics

Several ranking metrics were used to evaluate the recommendation system.

## Precision@K

Measures the proportion of recommended items that were relevant.

The following values of K were evaluated:

```text
K = 1, 3, 5, 10, 20
```

For `K=10`, the hybrid system achieved approximately:

```text
Precision@10 = 0.0160
```

while the popularity baseline achieved:

```text
Precision@10 = 0.0159
```

---

## Recall@K

Measures the proportion of relevant items that were successfully retrieved.

For `K=10`:

```text
Recall@10 ≈ 0.0075
```

---

## MAP@K

Mean Average Precision considers both the relevance of recommendations and their position within the ranking.

For `K=10`:

```text
MAP@10 ≈ 0.0054
```

---

## F1@K

Combines Precision and Recall using their harmonic mean.

For `K=10`:

```text
F1@10 ≈ 0.0102
```

---

# 📊 11. Comparison Against a Popularity Baseline

The hybrid system was compared against a simple popularity-based recommendation strategy.

Main results:

| Metric       | Hybrid Model | Popularity |
| ------------ | -----------: | ---------: |
| Precision@1  |       0.0145 |     0.0175 |
| Precision@3  |       0.0152 |     0.0165 |
| Precision@5  |       0.0159 |     0.0158 |
| Precision@10 |   **0.0160** |     0.0159 |
| Precision@20 |   **0.0159** |     0.0150 |
| Recall@10    |       0.0075 |     0.0082 |
| MAP@10       |       0.0054 |     0.0054 |

The results show that the hybrid system achieves a small improvement over popularity for some values of K, particularly as the recommendation list becomes larger.

---

# 📉 12. Statistical Significance

A paired comparison between the hybrid model and the popularity baseline showed that the observed differences in Precision@5 and Precision@10 were **not statistically significant**.

For Precision@10:

```text
Mean difference = +0.0003
p-value = 0.8046
```

Therefore, the results do not provide sufficient statistical evidence to conclude that the hybrid system significantly outperforms the popularity baseline on this dataset.

This analysis is important because it goes beyond simply reporting evaluation metrics and examines whether the observed improvement is statistically meaningful.

---

# 🔬 13. Sensitivity Analysis

The effect of changing the number of neighbors used by the collaborative filtering component was evaluated:

```text
k = 5
k = 10
k = 20
k = 50
k = 100
```

Precision@10 remained almost unchanged:

```text
0.0191 – 0.0192
```

This stability is related to the high sparsity of the user-item interaction matrix.

The matrix contains approximately:

```text
99.2% sparsity
```

As a result, increasing the number of neighbors does not produce a significant improvement.

The selected standard value is:

```text
k_neighbors = 20
```

---

# 💡 14. Recommendation Explainability

The system is not designed as a complete black box.

An explainability function was implemented:

```python
explicar_recomendacion(show_id, user_id)
```

This function analyzes the contribution of each recommendation component.

The explanation considers:

* Collaborative filtering contribution.
* Content-based contribution.
* Business rule contribution.

The final score can be represented as:

```text
Collaborative Filtering Contribution
+
Content-Based Contribution
+
Business Rules Contribution
=
Final Recommendation Score
```

This makes it possible to understand **why a specific title was recommended**.

---

# 📌 15. Key Findings

## 1. Content-Based Filtering has the strongest contribution

The best weight configuration was:

```text
α = 0.1
β = 0.8
γ = 0.1
```

This indicates that content characteristics, particularly genre-based information, were highly useful for this dataset.

---

## 2. Collaborative Filtering has limited contribution

The experiments showed approximately:

```text
Collaborative Filtering only
Precision@10 ≈ 0.0023
```

compared with:

```text
Content-Based only
Precision@10 ≈ 0.0193
```

The high sparsity of the user-item matrix limits the effectiveness of collaborative filtering.

---

## 3. Popularity is a strong baseline

The hybrid model produced results very close to the popularity baseline.

This demonstrates why recommendation systems should always be evaluated against a simple baseline before claiming significant improvements.

---

## 4. High Interaction Sparsity

The user-item matrix contains approximately:

```text
99.2% sparsity
```

This makes it difficult for collaborative filtering to identify enough meaningful relationships between users and content.

---

# ⚠️ 16. Limitations

The project has several limitations:

* High sparsity in the user-item matrix.
* Strong dependence on Content-Based Filtering.
* Some users have limited interaction history.
* Popularity is a difficult baseline to outperform.
* Precision@K remains relatively low.
* The test set represents only a specific temporal period.
* The Content-Based component relies primarily on genre information.
* Evaluation was performed on a sample of users due to computational constraints.

These limitations should be considered when interpreting the model's performance.

---

# 🚀 17. Future Improvements

Potential future improvements include:

* Incorporating descriptions, actors, and directors into the Content-Based model.
* Using text embeddings to represent content.
* Implementing matrix factorization.
* Implementing Alternating Least Squares (ALS).
* Testing neural recommendation models.
* Incorporating more detailed temporal features.
* Using sequential recommendation models.
* Automated hyperparameter optimization.
* Incorporating implicit feedback.
* Developing a real-time recommendation API.
* Building an interactive recommendation dashboard.
* Deploying the system using Streamlit or Gradio.

---

# 🛠️ Technologies

| Technology       | Purpose                                      |
| ---------------- | -------------------------------------------- |
| Python           | Main programming language                    |
| Pandas           | Data manipulation and cleaning               |
| NumPy            | Numerical computation                        |
| Scikit-learn     | Machine learning and similarity calculations |
| SciPy            | Statistical analysis                         |
| Matplotlib       | Data visualization                           |
| Seaborn          | Statistical visualization                    |
| Plotly           | Interactive visualization                    |
| Google Colab     | Development environment                      |
| Jupyter Notebook | Analysis and documentation                   |

---

# 📦 Installation

Clone the repository:

```bash
git clone <REPOSITORY_URL>
```

Navigate to the project directory:

```bash
cd Netflix-Recommendation-System
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

Open the main notebook:

```text
notebooks/ProyectoFinalFINALISIMO.ipynb
```

The project can also be executed directly in Google Colab.

---

# ▶️ Project Workflow

The complete workflow can be summarized as:

```text
Raw Data
   ↓
Exploratory Data Analysis
   ↓
Data Quality Analysis
   ↓
Data Cleaning
   ↓
Processed Data
   ↓
User Profiling
   ↓
Catalog Analysis
   ↓
User-Item Matrix
   ↓
Collaborative Filtering
   ↓
Content-Based Filtering
   ↓
Business Rules
   ↓
Hybrid Blender
   ↓
Recommendations
   ↓
Evaluation
   ↓
Explainability
```

---

# 📁 Project Deliverables

The project includes:

* Complete data analysis notebook.
* Data quality analysis.
* Data cleaning process.
* Exploratory data analysis.
* User profiling.
* Catalog analysis.
* Hybrid recommendation system.
* Item-based collaborative filtering.
* Content-based filtering.
* TF-IDF representation.
* Cold-start strategy.
* Business rules.
* Precision@K evaluation.
* Recall@K evaluation.
* MAP@K evaluation.
* F1@K evaluation.
* Temporal validation.
* Sensitivity analysis.
* Weight calibration.
* Statistical significance analysis.
* Recommendation explainability.

---

# 👨‍💻 Authors

**Allyson Daniela García Castro**
**Sergio Andrés Rodríguez Víquez**
**Jose Alberto Carranza Cedeño**

Academic project developed for:

**TAND-06 — Final Project**

---

# 📚 Concepts Applied

This project integrates concepts from:

* Data Cleaning
* Exploratory Data Analysis
* Data Profiling
* Feature Engineering
* Clustering
* Recommendation Systems
* Collaborative Filtering
* Content-Based Filtering
* TF-IDF
* Cosine Similarity
* Nearest Neighbors
* Cold-Start
* Ranking Systems
* Precision@K
* Recall@K
* MAP@K
* F1@K
* Temporal Validation
* Data Leakage Prevention
* Statistical Testing
* Hyperparameter Tuning
* Explainable Recommendation Systems

---

# ⭐ Conclusion

This project demonstrates the development of a complete recommendation system, from data preparation and exploratory analysis to modeling, evaluation, and explainability.

The proposed solution combines **collaborative filtering, content-based filtering, and business rules** to generate personalized and interpretable recommendations.

The results indicate that Content-Based Filtering is the strongest component for this particular dataset, while collaborative filtering is constrained by the high sparsity of user-item interactions.

Although the improvement over the popularity baseline is limited and not statistically significant, the project demonstrates a complete recommendation-system workflow including **data cleaning, hybrid modeling, temporal validation, ranking evaluation, weight calibration, sensitivity analysis, and explainability**.
