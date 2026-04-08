# 🔍 ArXiv Topic Discovery — Research Paper Abstract Mining (Assignment No. 1)

> **Unsupervised topic modelling on 100 K+ arXiv abstracts using LDA, NMF, TF-IDF, and t-SNE — no labels required.**

Exponential growth in research publications makes manual categorisation impractical. This project automatically discovers latent research themes directly from raw abstracts, enabling faster literature navigation, trend detection, and knowledge discovery.

---
**Project Members-**
-Yash Rai- BTECH/10502/23
-Tanishk Thakur - BTECH/10502/23
-Aryan Nahata- BTECH/10823/23
-Tejas Ganesh- BTECH/10381/23
-Om Gupta- BTECH/10638/23

---

## 📑 Table of Contents

1. [Project Overview](#-project-overview)
2. [Repository Structure](#-repository-structure)
3. [Dataset Setup](#-dataset-setup)
4. [Environment Setup](#-environment-setup)
5. [Execution Order](#-execution-order)
6. [Notebook Reference](#-notebook-reference)
7. [Results & Key Findings](#-results--key-findings)
8. [Ethical Considerations](#-ethical-considerations)
9. [License](#-license)

---

## 🧭 Project Overview

| Item | Detail |
|------|--------|
| **Task** | Unsupervised latent topic discovery |
| **Dataset** | arXiv (Cornell University) via Kaggle |
| **Subset used** | ~100,000 abstracts (sampled) |
| **Models** | TF-IDF · LDA · NMF · t-SNE |
| **Assignment** | USL Lab — Assignment 1 |
| **Language** | Python 3.10+ |

### Pipeline at a glance

```
Raw JSON abstracts
      │
      ▼
01_Preprocessing       ← clean, tokenise, lemmatise
      │
      ▼
02_Feature_Engineering ← TF-IDF matrix + word embeddings
      │
      ▼
03_Topic_Modeling      ← LDA (Gensim) + NMF (sklearn)
      │
      ▼
04_Visualization_tSNE  ← t-SNE scatter + pyLDAvis
      │
      ▼
05_Interpretation_Ethics ← coherence scores, dominant themes, ethical reflection
```

---

## 📁 Repository Structure

```
arXiv-Topic-Discovery/
│
├── data/                          # ← NOT tracked in git (3–4 GB)
│   └── arxiv-metadata-oai-snapshot.json
│
├── notebook/
│   ├── 01_Preprocessing.ipynb         # Text cleaning & tokenisation
│   ├── 02_Feature_Engineering.ipynb   # TF-IDF vectorisation & embeddings
│   ├── 03_Topic_Modeling.ipynb        # LDA & NMF topic models
│   ├── 04_Visualization_tSNE.ipynb    # t-SNE & pyLDAvis plots
│   └── 05_Interpretation_Ethics.ipynb # Results interpretation & ethics
│
├── .gitignore
├── LICENSE
├── README.md
├── Presentation.pptx
└── requirements.txt
```

> **Why is `data/` empty on GitHub?**
> The arXiv snapshot JSON is ~3–4 GB. It is listed in `.gitignore` to keep the repo lightweight. See [Dataset Setup](#-dataset-setup) below to download it.

---

## 📦 Dataset Setup

1. Go to the Kaggle dataset page:
   **[https://www.kaggle.com/datasets/Cornell-University/arxiv](https://www.kaggle.com/datasets/Cornell-University/arxiv)**

2. Download `arxiv-metadata-oai-snapshot.json` (~3.4 GB compressed).

3. Place the file inside the `data/` folder:

```
arXiv-Topic-Discovery/
└── data/
    └── arxiv-metadata-oai-snapshot.json   ✅
```

4. *(Optional)* To download via the Kaggle CLI:

```bash
# Install CLI if needed
pip install kaggle

# Place kaggle.json API token at ~/.kaggle/kaggle.json, then:
kaggle datasets download -d Cornell-University/arxiv --unzip -p data/
```

---

## ⚙️ Environment Setup

### Python Version

```
Python 3.10.x  (recommended)
Python 3.9.x   (compatible)
Python 3.11.x  (compatible, tested)
```

> Python 3.12+ may have minor compatibility issues with `pyLDAvis`. Stick to **3.10** for a friction-free experience.

---

### Option A — pip (recommended for most users)

```bash
# 1. Clone the repo
git clone https://github.com/yash-rai-93/arXiv-Topic-Discovery.git
cd arXiv-Topic-Discovery

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate          # macOS / Linux
venv\Scripts\activate             # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Download NLTK data (run once)
python -c "import nltk; nltk.download('stopwords'); nltk.download('wordnet'); nltk.download('omw-1.4')"
```

---

### Option B — Conda

```bash
conda create -n arxiv-topics python=3.10 -y
conda activate arxiv-topics
pip install -r requirements.txt
python -c "import nltk; nltk.download('stopwords'); nltk.download('wordnet'); nltk.download('omw-1.4')"
```

---

### Core Library Versions

| Library | Recommended Version | Notes |
|---------|---------------------|-------|
| `numpy` | `1.24.x` | `1.25+` works but may warn on older gensim |
| `pandas` | `2.0.x` | Used for data loading and sampling |
| `scikit-learn` | `1.3.x` | NMF, TF-IDF, train/test splits |
| `gensim` | `4.3.x` | LDA model + coherence scores |
| `nltk` | `3.8.x` | Stopwords, lemmatisation |
| `matplotlib` | `3.7.x` | Base plotting |
| `seaborn` | `0.12.x` | Statistical visualisations |
| `pyLDAvis` | `3.4.x` | Interactive LDA topic explorer |
| `scikit-learn` | `1.3.x` | TF-IDF vectoriser, NMF |
| `scipy` | `1.11.x` | Sparse matrix operations |
| `tqdm` | `4.65.x` | Progress bars during preprocessing |
| `jupyter` | `1.0.x` | Notebook runtime |
| `ipywidgets` | `8.x` | Interactive widgets in notebooks |

All pinned versions are listed in `requirements.txt`. Run `pip install -r requirements.txt` to get exact reproducible versions.

---

### Launch Jupyter

```bash
jupyter notebook
# or
jupyter lab
```

Then open notebooks in the order described below.

---

## 🚀 Execution Order

**Notebooks must be run strictly in the numbered order.** Each notebook saves intermediate outputs (cleaned text, TF-IDF matrices, trained models) that are consumed by the next.

```
┌─────────────────────────────────────────────────────────────┐
│  STEP 1  →  notebook/01_Preprocessing.ipynb                 │
│  STEP 2  →  notebook/02_Feature_Engineering.ipynb           │
│  STEP 3  →  notebook/03_Topic_Modeling.ipynb                │
│  STEP 4  →  notebook/04_Visualization_tSNE.ipynb            │
│  STEP 5  →  notebook/05_Interpretation_Ethics.ipynb         │
└─────────────────────────────────────────────────────────────┘
```

### Quick-start commands (run all headlessly)

```bash
cd notebook

jupyter nbconvert --to notebook --execute 01_Preprocessing.ipynb --output 01_Preprocessing.ipynb
jupyter nbconvert --to notebook --execute 02_Feature_Engineering.ipynb --output 02_Feature_Engineering.ipynb
jupyter nbconvert --to notebook --execute 03_Topic_Modeling.ipynb --output 03_Topic_Modeling.ipynb
jupyter nbconvert --to notebook --execute 04_Visualization_tSNE.ipynb --output 04_Visualization_tSNE.ipynb
jupyter nbconvert --to notebook --execute 05_Interpretation_Ethics.ipynb --output 05_Interpretation_Ethics.ipynb
```

> ⚠️ Step 3 (topic modelling) can take **10–30 minutes** depending on your hardware and the number of LDA iterations set. All other steps complete in under 5 minutes each.

---

## 📓 Notebook Reference

### `01_Preprocessing.ipynb` — Text Cleaning

**Input:** `data/arxiv-metadata-oai-snapshot.json`
**Output:** `data/cleaned_abstracts.csv`

What it does:
- Loads and samples ~100,000 abstracts from the full JSON snapshot
- Lowercases all text and normalises unicode characters
- Removes URLs, numbers, punctuation, and special symbols
- Tokenises text at word level
- Removes English stopwords using NLTK's corpus
- Lemmatises tokens using `WordNetLemmatizer`
- Filters out tokens shorter than 3 characters
- Saves the cleaned token lists to CSV for downstream use

Key parameters to tune:
```python
SAMPLE_SIZE = 100_000     # Number of abstracts to sample
MIN_TOKEN_LEN = 3         # Minimum token length to keep
```

---

### `02_Feature_Engineering.ipynb` — Feature Extraction

**Input:** `data/cleaned_abstracts.csv`
**Output:** `data/tfidf_matrix.npz`, `data/tfidf_vocab.pkl`, `data/corpus_gensim.pkl`, `data/dictionary_gensim.pkl`

What it does:
- Builds a TF-IDF sparse matrix using `sklearn.feature_extraction.text.TfidfVectorizer`
- Applies `min_df=5, max_df=0.85` to filter rare and overly common terms
- Builds a Gensim `Dictionary` and Bag-of-Words corpus for LDA
- Saves all artefacts for use in notebook 03

Key parameters to tune:
```python
MAX_FEATURES = 10_000     # Vocabulary size cap for TF-IDF
MIN_DF = 5                # Minimum document frequency
MAX_DF = 0.85             # Maximum document frequency (fraction)
```

---

### `03_Topic_Modeling.ipynb` — LDA & NMF

**Input:** `data/tfidf_matrix.npz`, `data/corpus_gensim.pkl`, `data/dictionary_gensim.pkl`
**Output:** `data/lda_model/`, `data/nmf_model.pkl`, `data/doc_topic_matrix.npy`

What it does:
- Trains a **Latent Dirichlet Allocation** model using `gensim.models.LdaMulticore` (parallelised)
- Trains a **Non-Negative Matrix Factorisation** model using `sklearn.decomposition.NMF`
- Evaluates both models using **coherence score (c_v)** via `gensim.models.CoherenceModel`
- Prints the top-10 keywords per topic for human interpretation
- Saves the document–topic distribution matrix (`doc_topic_matrix.npy`) for t-SNE

Key parameters to tune:
```python
NUM_TOPICS = 10           # Number of latent topics K
LDA_PASSES = 15           # Training passes over the corpus
LDA_ITERATIONS = 100      # Per-document inference iterations
ALPHA = 'auto'            # Document-topic prior (auto-tuned)
ETA = 'auto'              # Topic-word prior (auto-tuned)
```

---

### `04_Visualization_tSNE.ipynb` — Cluster Visualisation

**Input:** `data/doc_topic_matrix.npy`, `data/lda_model/`
**Output:** Interactive HTML plots (pyLDAvis), t-SNE scatter plots

What it does:
- Applies **t-SNE** (`sklearn.manifold.TSNE`) to the document–topic matrix to reduce it to 2-D
- Colour-codes each document point by its dominant topic
- Renders an interactive **pyLDAvis** dashboard showing topic-word relevance and inter-topic distance
- Plots topic-word bar charts showing the top keywords per topic

Key parameters to tune:
```python
TSNE_PERPLEXITY = 40      # t-SNE perplexity (typically 5–50)
TSNE_N_ITER = 1000        # t-SNE optimisation iterations
TSNE_RANDOM_STATE = 42    # Reproducibility seed
```

---

### `05_Interpretation_Ethics.ipynb` — Interpretation & Ethics

**Input:** All prior outputs
**Output:** Final summary tables, coherence comparison charts

What it does:
- Summarises and labels discovered topics based on top keywords
- Compares LDA vs NMF coherence scores side-by-side
- Identifies dominant and emerging research areas across arXiv categories
- Discusses **ethical considerations**: bias in topic emergence, fairness, data privacy, and societal impact of automated topic discovery

---

## 📊 Results & Key Findings

| Model | Coherence Score (c_v) |
|-------|----------------------|
| LDA (K=10) | ~0.52 |
| NMF (K=10) | ~0.61 |

### Discovered Topics (sample, K = 10)

| Topic | Top Keywords | Inferred Theme |
|-------|-------------|----------------|
| 1 | neural, network, model, layer, training, deep | Deep Learning |
| 2 | quantum, state, system, energy, measurement | Quantum Physics |
| 3 | graph, node, edge, algorithm, network | Graph Theory |
| 4 | protein, structure, gene, sequence, expression | Bioinformatics |
| 5 | language, model, text, generation, transformer | NLP / LLMs |
| 6 | image, classification, detection, visual, feature | Computer Vision |
| 7 | market, economic, model, prediction, risk | Finance / Economics |

> Topic labels are manually assigned by inspecting the top keywords — the model outputs the keywords, not the labels.

---

## 🤝 Ethical Considerations

- **No annotator bias** — topics emerge purely from data; no human label subjectivity is introduced.
- **Fair representation** — unsupervised discovery surfaces under-represented sub-fields that curated taxonomies may overlook.
- **Privacy** — the pipeline uses only publicly available arXiv abstracts. No personal or private data is involved.
- **Transparency** — all model parameters, preprocessing steps, and evaluation metrics are fully documented and reproducible.
- **Limitations** — topic coherence and interpretability depend on corpus size and pre-processing quality. Topics may merge or split at different K values.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

The arXiv dataset is provided by Cornell University under its own terms of service. See [Kaggle — arXiv Dataset](https://www.kaggle.com/datasets/Cornell-University/arxiv) for licensing details.

---

*Built as part of USL Lab — Assignment 1: Research Paper Topic Discovery Using Abstract Mining.*
