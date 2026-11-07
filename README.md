# Healthcare Question Answering with Semantic Search and NLP

A medical information retrieval and summarization prototype that combines sentence embeddings, similarity search, and answer summarization to build an interactive healthcare chatbot.

## Overview

This project demonstrates semantic search and text summarization applied to medical question answering. It uses a MedQuAD dataset of medical questions and answers, encodes them with sentence transformers, and retrieves the most relevant answer for a user's query before summarizing it for readability.

The application is a development prototype intended for learning and demonstration.

## How It Works

The chatbot has two main paths:

| User input | What the code does |
|---|---|
| Contains `?` | Finds the most similar stored question and summarizes its answer |
| Does not contain `?` | Searches stored answers for matching text and returns the associated disease |

For example, `What is Parkinson's disease?` goes through semantic retrieval. A symptom description without a question mark goes through text matching.

## Dataset

The notebook loads a MedQuAD CSV with the following recorded characteristics:

| Item | Recorded value |
|---|---:|
| Original rows | 16,412 |
| Original columns | Question, answer, source, disease |
| Distinct disease labels | 5,126 |
| Missing answers | 5 |
| Missing disease labels | 14 |

Preprocessing includes duplicate removal, missing-value handling, lowercasing, number removal, tokenization, lemmatization, stopword removal, and trigram exploration.

## Models and Components

| Component | Actual use |
|---|---|
| `all-MiniLM-L6-v2` | Creates embeddings to match user questions with dataset questions |
| Cosine similarity | Selects the closest stored question |
| Summarization pipeline | Shortens the selected answer |
| BERT QA model | Extracts answer spans in two separate example experiments |
| Word2Vec | Attempted embedding experiment |

The core retrieval workflow uses **sentence embeddings, similarity search, and answer summarization**.

## Strengths

- Addresses a clear information-retrieval problem.
- Demonstrates several NLP techniques in one notebook.
- Semantic matching accommodates wording differences between user and stored questions.
- Summarization makes long dataset answers easier to read.
- Saved conversations demonstrate an interactive prototype.
- The presentation provides useful background and a description of the intended application.

## Known Limitations

| Priority | Issue |
|---|---|
| High | No similarity threshold — even unrelated questions receive the closest available answer |
| High | No formal evaluation metrics (accuracy, Recall@k, MRR) |
| Medium | All question embeddings are recomputed per query |
| Medium | Routing depends on `?` punctuation |
| Medium | Dataset and dependencies are not packaged reproducibly |

## Future Improvements

1. Keep original answers and source metadata unchanged; create separate text fields for search.
2. Calculate question embeddings once and cache them.
3. Retrieve by row index so the selected question stays linked to its answer and source.
4. Add a similarity threshold and an explicit "no suitable answer found" response.
5. Replace punctuation-based routing with an explicit interaction mode.
6. Evaluate retrieval using held-out paraphrased questions, Recall@k, and MRR.
7. Check summary faithfulness, including preservation of numbers and qualifications.
8. Include dataset acquisition instructions, dependency versions, and a clean notebook.

## Technology Stack

- Python
- Jupyter Notebook
- Sentence Transformers (`all-MiniLM-L6-v2`)
- Hugging Face Transformers (summarization pipeline, BERT QA)
- scikit-learn (cosine similarity)
- NLTK (tokenization, lemmatization, stopwords)
- Gensim (Word2Vec)
- Pandas, NumPy

## Project Structure

| File | Purpose |
|---|---|
| `Copy of NLP Project 1st copy.ipynb` | Main notebook with all code, experiments, and chatbot |
| `Healthcare chatbot.pptx` | Nine-slide presentation describing the project |


