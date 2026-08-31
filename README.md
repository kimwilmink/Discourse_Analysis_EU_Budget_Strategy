# Discourse Analysis: EU Budget Strategy

This Master's thesis project analyses whether EU-funded research project descriptions (Horizon 2020 and Horizon Europe) show a discursive shift from climate-oriented narratives toward security- and resilience-oriented narratives.

**Research question:** Has there been a discursive shift in EU-funded project descriptions from climate-oriented narratives to security- and resilience-oriented narratives?

**Research plan:**
- Inspect keyword frequency trends over the years (e.g. "climate", "sustainability" vs. "security", "resilience", "strategic autonomy")
- Topic modeling (BERTopic) to identify thematic clusters per year, then compare clusters over time
- Combine bag-of-words frequency analysis with sentence-embedding-based topic modelling via BERTopic

The analysis uses each project's keywords, title, and objective (`metadata_freeKeywords`, `metadata_title`, `metadata_objective`).

## Data

Project data is retrieved from the European Commission's [SEDIA](https://ec.europa.eu/info/funding-tenders/opportunities/portal/screen/home) portal with the [`sedia-api-fetchers`](https://pypi.org/project/sedia-api-fetchers/) package, covering both the Horizon 2020 and Horizon Europe funding programmes.

Due to the data's large file size, it was not uploaded to Github. The rest of the plots that were created in the notebooks, however, are in the data folder.

## Setup

```bash
pip install -r requirements.txt
```

The notebooks also require the NLTK `punkt`, `punkt_tab`, `stopwords`, and `wordnet` corpora, e.g.:

```python
import nltk
nltk.download("punkt")
nltk.download("punkt_tab")
nltk.download("stopwords")
nltk.download("wordnet")
```

## Notebooks

Run in this order:

1. **`import_data.ipynb`** - Fetches Horizon 2020 and Horizon Europe project data with the `sedia-api-fetchers` library, and saves the raw and combined datasets to `data/`.
2. **`eda_and_preprocessing.ipynb`** — Exploratory analysis and text preprocessing: word cloud of most frequent terms and project start/end dates and duration.
3. **`bow_and_bertopic_analysis.ipynb`** — Main analysis notebook:
   - Bag-of-words keyword frequency trends (climate vs. security/resilience dictionaries) performed on both the full corpus and the climate-specific subset
   - A robustness check based on the share of projects mentioning each narrative
   - BERTopic topic modelling, validated on a sample and then fit on the full climate-specific corpus
   - Year-by-year comparison of topic prevalence and representative documents per topic

## Outputs

Data fetched from the API and generated figures (png) are saved to `data/` (csv file with the fetched Hprizon 2020 and Horizon Europe data, word cloud, date-distribution histograms, BERTopic topic-frequency, yearly-evolution plots, etc.).
