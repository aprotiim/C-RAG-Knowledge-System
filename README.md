# Corrective Retrieval Augmented Generation (CRAG)

Implementation of the research paper:

**Corrective Retrieval Augmented Generation**
https://arxiv.org/pdf/2401.15884

This project implements CRAG, a framework designed to improve Retrieval-Augmented Generation (RAG) systems by detecting incorrect retrieval results and correcting them before generation.

CRAG improves RAG by introducing:

* Retrieval evaluation

* Corrective retrieval

* Knowledge refinement

The system ensures that LLMs only generate answers using reliable knowledge.

## Problem with Standard RAG

Standard RAG pipelines assume the retriever always returns relevant documents.

However, retrieval can fail due to:

* irrelevant documents

* outdated information

* incomplete context

When this happens, the LLM produces hallucinated answers.

## Standard RAG Architecture
<img width="2561" height="945" alt="image" src="https://github.com/user-attachments/assets/71efc2b9-e8b9-4658-b592-d056c2e11532" />

**Issue** - The retriever has no mechanism to verify retrieval quality, which can lead to hallucinations.

## Corrective RAG Architecture

<img width="832" height="570" alt="image" src="https://github.com/user-attachments/assets/533bdf9d-9422-454f-a054-facd53d3e34c" />

## Retrieval Evaluator (Core Idea of CRAG)

CRAG introduces a lightweight retrieval evaluator that estimates the quality of retrieved documents.
It assigns a confidence category:

* Correct

* Incorrect

* Ambiguous

Based on this evaluation, the system decides how to proceed.

## Knowledge Refinement

Even when retrieval is correct, documents often contain irrelevant text.

CRAG introduces a Decompose-Then-Recompose algorithm.

This algorithm:

* Decomposes documents into smaller units

* Filters irrelevant information

* Recombines useful knowledge

## Complete CRAG Inference Pipeline
<img width="1329" height="1557" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/74549e38-b512-4f1c-a4d5-075244f2fc82" />

## Advantages of CRAG

CRAG improves traditional RAG systems by:

* detecting low-quality retrieval

* correcting knowledge using web search

* refining document context

* reducing hallucinations

Experiments in the paper show significant improvements across multiple QA and generation tasks.

## Tech Stack

* Python

* LangChain

* FAISS

* OpenAI

* Jupyter

## Summary

CRAG enhances traditional RAG by introducing:

1. Retrieval Evaluation

2. Corrective Retrieval

3. Knowledge Refinement

This allows LLM systems to detect and fix retrieval errors before generation, significantly improving reliability.
