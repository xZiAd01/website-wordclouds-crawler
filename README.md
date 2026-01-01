# Website WordClouds (Crawler + Text Extractor)

A lightweight web crawler that starts from a given URL, visits a limited number of pages, extracts the main readable text from each page, tokenizes/cleans English words (with stopword removal), then generates **word cloud images** and a **CSV summary**.

## What it does
- Crawls pages starting from `START_URL` (BFS-style queue)
- Resolves relative links and avoids revisiting the same URL
- Extracts the “readable” article/body text (not menus/headers) using `readability`
- Cleans and tokenizes English text (filters short tokens, punctuation, numbers, stopwords)
- Produces:
  - WordCloud image per page (`.png`)
  - CSV file listing pages and word counts / filenames

## Outputs
By default, everything is saved under:
- `out_crawl/`
  - `wordclouds/` (PNG files)
  - `pages.csv` (summary table)

> The exact structure matches the notebook logic (output folder names come from `OUT_DIR`).

## Configuration
Edit these variables in the notebook:

```python
START_URL = "https://www.bbc.com/"   # The site to start crawling
MAX_PAGES = 20                       # Maximum number of pages to visit
MIN_WORDS = 500                      # Minimum words required for a page to be analyzed
DELAY = 0.5                          # Seconds to wait between requests (politeness)
OUT_DIR = "out_crawl"                # Folder to store outputs
```
## Notes on configuration (don’t ignore this)

`MAX_PAGES` ≠ “complete crawl”. Many sites have thousands of internal links; keep it small.

`MIN_WORDS` can silently discard pages (homepages and category pages often fail it). If you see “No pages found”, lower it.

`DELAY` matters. Setting it to 0 is a quick way to get blocked.

## Quick start (local)

# 1. Create a venv (recommended)
```bash
python -m venv .venv
source .venv/bin/activate  # mac/linux
# .venv\Scripts\activate   # windows
```
# 2. Install dependencies
```bash
pip install -r requirements.txt
```
# 3. Run the notebook
```bash
jupyter notebook
```
Open Assinment_4_notebook.ipynb, adjust START_URL, and run all cells.
## Dependencies
- requests
- beautifulsoup4
- readability-lxml
- nltk
- pandas
- wordcloud
- matplotlib

The notebook auto-downloads NLTK stopwords if missing.
