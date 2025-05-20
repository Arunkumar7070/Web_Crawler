# Web Crawler and Search Engine  
**Author**: Arun Kumar  
**College**: PSG College of Technology  
**GitHub**: [arunganesh7070@gmail.com](mailto:arunganesh7070@gmail.com)

## About  
This project is a custom web crawler and search engine that I developed in Python 3 during my time at PSG College of Technology. My goal was to gain hands-on experience in data structures, algorithms, and information retrieval systems.

The crawler is designed to navigate and process content from academic websites and extract meaningful information. The search engine component enables querying through the crawled data using cosine similarity and supports document clustering and synonym expansion via a thesaurus.

## Key Features

- **Web Crawling**: The crawler navigates through web pages starting from a seed URL, extracts content, and respects `robots.txt` policies to ensure ethical scraping.
- **Indexing**: Each visited page is processed and added to an in-memory index. Pages are hashed to detect duplicates, and a term frequency matrix is constructed.
- **Stemming**: All extracted words are stemmed using the NLTK Porter Stemmer to normalize content.
- **Document Clustering**: Pages are grouped using a simple leader-based clustering algorithm based on Euclidean distance.
- **Search Engine**: 
  - Queries are matched against the indexed content using LTC.LTC weighted cosine similarity.
  - Stopwords are filtered out using a configurable stopword list.
  - If few results are returned, synonym expansion is performed using a thesaurus to improve recall.
  - Documents with query terms in the title get a slight score boost.
- **Query Output**: Top results are displayed with relevance scores, titles, and snippet previews.

## How It Works

### Crawler
The crawler begins at a specified seed URL and builds a queue (`url_frontier`) of unvisited links. It visits pages one by one, collecting:
- Page titles
- Valid words (filtered by regex and stemmed)
- Outgoing, broken, and image links
- Duplicate content based on content hashing

Each page is assigned a unique document ID and stored along with its metadata. The crawler generates a complete term frequency matrix and exports results such as:
- Top 20 stemmed words with document frequencies
- Document clusters
- Term frequency matrix as CSV
- Optionally, an index file for later re-use

### Search Engine
The search engine builds upon the crawler and adds:
- Import/export functionality for indices
- Query processing and result ranking
- Document clustering for faster search
- Query expansion using a user-provided thesaurus

When a user submits a query:
- Stopwords are removed
- Remaining words are stemmed and matched to the index
- Cosine similarity is calculated using the LTC.LTC weighting scheme
- If results are few, synonyms are used to reformulate the query
- Top results (with scores > 0) are shown, sorted by relevance
