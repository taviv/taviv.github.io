---
layout: page
title: Clinical Drug Monograph RAG
description: Retrieval-Augmented Generation over a TNF-alpha inhibitor monograph using Gemini and ChromaDB
img: assets/img/11.jpg
importance: 2
category: work
related_publications:
---

## What It Does

A Retrieval-Augmented Generation (RAG) pipeline that lets you ask plain-language clinical questions about a drug monograph and get answers grounded strictly in the document. Built over a TNF-alpha inhibitor monograph as a concrete healthcare example.

Sample queries it answers correctly:
- *What is the initiation dose?*
- *What are the contraindications?*
- *What is the most severe potential side effect?*
- *What doses are available?*

## Why It's Interesting

Drug monographs are dense, technical, and long. Clinicians and pharmacists reference them frequently but navigating them is slow. A RAG layer turns a static PDF into an interactive Q&A surface — with answers that cite only what's in the document, not hallucinated general knowledge.

The `task_type` distinction in the Gemini embedding API — `retrieval_document` for indexing, `retrieval_query` for querying — is a meaningful quality lever that most naive RAG implementations miss. The pipeline also uses a character budget on retrieved context to control generation cost, and a grounded prompt that restricts the model to retrieved chunks only.

## Stack

- **Embeddings:** Google Gemini `gemini-embedding-001` (document + query optimized task types)
- **Vector store:** ChromaDB (persistent)
- **Generation:** Gemini 2.5 Flash
- **Document loading:** LangChain + PyPDF + Google Cloud Storage
- **Chunking:** RecursiveCharacterTextSplitter (1,000 chars, 100 overlap)

## Notebook

The full implementation is available as a Colab-ready notebook:

[View notebook on GitHub](https://github.com/taviv/taviv.github.io/blob/master/assets/jupyter/tnf_rag.ipynb)

## Next Steps

- **Chunking by page first** to avoid splitting mid-sentence across clinical sections
- **Biomedical embeddings** (MedCPT, BiomedBERT) for better clinical terminology retrieval vs general-purpose Gemini embeddings
- **Multi-document** extension across a full drug class (all TNF inhibitors) for comparative Q&A
- **Evaluation layer** with a gold-standard Q&A set to measure retrieval precision and answer accuracy
