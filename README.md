Scientific Paper Intelligence System
An end-to-end data science and natural-language-processing project for organizing and exploring scientific research papers. It combines classification, clustering, content-based recommendation, and retrieval-based question answering using titles and abstracts from an arXiv dataset.
Project highlights
Processed 287,421 research papers
Worked with 146 original scientific categories
Created Bag-of-Words and TF-IDF text features
Compared Logistic Regression, Multinomial Naive Bayes, and LinearSVC
Applied K-Means clustering and Truncated SVD visualization
Built a cosine-similarity research-paper recommender
Built a retrieval-based QA component using abstract sentences
Dataset
The project uses the arXiv Scientific Research Papers Dataset from Kaggle:
https://www.kaggle.com/datasets/sumitm004/arxiv-scientific-research-papers-dataset
The main fields used are `title`, `summary`, and `category`. The first notebook downloads the dataset, so the large CSV files are not uploaded to GitHub.
Repository files
```text
scientific-paper-intelligence-system/
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
├── 01_Data_Loading_Cleaning.ipynb
├── 02_Text_Preprocessing.ipynb
├── 03_Feature_Engineering.ipynb
├── 04_Classification.ipynb
├── 05_Clustering.ipynb
├── 06_Recommendation_QA.ipynb
└── results/
```
Workflow
1. Data loading and cleaning
Downloads the Kaggle dataset, inspects the schema, checks duplicates and missing values, cleans text fields, converts dates, recalculates abstract word counts, and saves `cleaned_arxiv_datasets.csv`.
2. Text preprocessing
Combines titles and abstracts, converts text to lowercase, removes punctuation and stop words, applies WordNet lemmatization, and saves `preprocessed_dataset.csv`. The completed run produced 287,421 rows and 12 columns.
3. Feature engineering
Creates 5,000-feature Bag-of-Words and TF-IDF matrices, compares the representations, visualizes important terms, and saves the selected TF-IDF features.
4. Classification
Categories with fewer than 150 papers are removed. The final experiment used 284,130 papers across 55 categories, with 227,304 training records and 56,826 testing records.
Model	Accuracy	Macro F1	Weighted F1
Logistic Regression	52.15%	34.00%	55.90%
Multinomial Naive Bayes	65.99%	14.18%	62.62%
LinearSVC	60.20%	34.32%	62.46%
Selected model: LinearSVC. It achieved the strongest macro F1-score and therefore provided the best balance across the retained categories.
![Classification model comparison](results/classification_model_comparison.png)
5. Clustering
Uses a 5,000-feature TF-IDF matrix and K-Means with 10 clusters. It tests 2–15 clusters with the elbow method, extracts the most important terms, and uses Truncated SVD for visualization.
Silhouette score: 0.0068. The low score indicates overlapping themes, which is reasonable because related scientific fields often share vocabulary.
![Cluster visualization](results/cluster_visualization_2d.png)
6. Recommendation and question answering
The recommendation system cleans a user query, converts it to TF-IDF, calculates cosine similarity against all papers, and returns the most relevant titles, categories, authors, abstracts, and similarity scores.
The QA component first retrieves candidate papers, then selects the abstract sentence most related to the question.
Component	Metric	Score	Test cases
Recommendation	Mean Precision@5	0.8000	4
Retrieval-based QA	Average keyword relevance	0.5333	5
These small test sets provide an initial demonstration rather than a complete benchmark.
Installation
```bash
python -m venv .venv
```
Windows:
```bash
.venv\Scripts\activate
```
macOS/Linux:
```bash
source .venv/bin/activate
```
Install the required packages:
```bash
pip install -r requirements.txt
```
Start Jupyter:
```bash
jupyter notebook
```
Run the notebooks in numerical order from `01` to `06`.
Technologies
Python, Pandas, NumPy, Scikit-learn, SciPy, NLTK, KaggleHub, Matplotlib, Jupyter, TF-IDF, Bag of Words, Logistic Regression, Multinomial Naive Bayes, LinearSVC, K-Means, Truncated SVD, and cosine similarity.
Limitations
Scientific categories are imbalanced.
Related fields use similar vocabulary.
TF-IDF does not capture deeper semantic meaning.
The clustering score shows substantial overlap.
Recommendation evaluation uses four queries only.
QA evaluation uses five questions only.
The QA system retrieves existing abstract sentences rather than generating full answers.
The system uses titles and abstracts instead of full papers.
Running the complete dataset requires substantial time and memory.
Suggested résumé description
Scientific Paper Intelligence System — Data Science and NLP
Developed an end-to-end NLP pipeline for 287,421 arXiv papers, covering data cleaning, text preprocessing, feature engineering, classification, clustering, recommendation, and retrieval-based question answering.
Compared Logistic Regression, Multinomial Naive Bayes, and LinearSVC across 55 categories using accuracy, macro F1, and weighted F1.
Applied K-Means and Truncated SVD to analyze research themes and built a TF-IDF recommender with Mean Precision@5 of 0.80.
Evaluated a retrieval-based QA component that selected relevant sentences from paper abstracts and documented its limitations.
License
The project code is released under the MIT License. The external Kaggle dataset remains subject to its original terms.
