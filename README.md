# Text Summarization with T5-Small

## Project Overview

This project implements a complete text summarization system using the T5-small Transformer model. It includes data preprocessing, exploratory data analysis (EDA), model fine-tuning on the CNN/DailyMail dataset, performance evaluation with ROUGE metrics, and deployment through an interactive Gradio interface. The system is capable of generating accurate and concise summaries from long-form news articles in real time.

## Why Use a Summarizer?

Text summarization is important because it helps:

- 🧠 Quickly extract key information from long documents
- ⏱ Save time by condensing large volumes of content
- 📚 Enhance reading comprehension and content curation
- 📈 Improve productivity in academic, legal, medical, and business domains
- 🤖 Enable downstream NLP tasks like indexing, retrieval, and question answering

Using a summarizer powered by a pre-trained Transformer like T5-small ensures high-quality results with efficient fine-tuning on specific datasets.

## Dataset Overview

The system uses the **CNN/DailyMail** dataset — a standard benchmark for abstractive summarization. It contains real-world news articles paired with human-written summaries.

- **Source**: CNN and Daily Mail news websites
- **Task**: Generate concise summaries from long-form articles
- **Language**: English
- **Dataset Size**: ~300,000 article-summary pairs
- **Article Length**: Typically 600–800 words
- **Summary Length**: Typically 50–70 words


---
## Tools used
Built with HuggingFace Transformers, Datasets, Evaluate, and Gradio.


