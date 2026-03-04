# C-RAG-Knowledge-System
Corrective RAG: Reducing Hallucinations in Retrieval-Augmented Generation

Implementation of Corrective Retrieval Augmented Generation (CRAG) from the research paper:

Corrective Retrieval Augmented Generation
https://arxiv.org/pdf/2401.15884

This project demonstrates how LLM hallucinations in standard RAG systems can be mitigated by evaluating retrieval quality and correcting the retrieval process dynamically.

Motivation

Large Language Models often hallucinate when:

retrieved documents are irrelevant

retrieved context is incomplete

retrieval systems fail to capture true intent of the query

Standard RAG assumes retrieved documents are always useful.

This assumption is incorrect.

Corrective RAG introduces a retrieval evaluator and correction loop that improves factual grounding.

Standard RAG vs Corrective RAG
Standard RAG Pipeline
4

Standard workflow:

User query

Query embedding

Vector database retrieval

Top-k documents retrieved

LLM generates answer

Problem

If retrieved documents are wrong → LLM hallucinates.

Corrective RAG Architecture
4

Corrective RAG adds a retrieval evaluator and correction mechanism.

Instead of trusting retrieved documents blindly, CRAG performs:

1️⃣ Document relevance evaluation
2️⃣ Decision routing
3️⃣ External knowledge retrieval if needed

CRAG Decision Flow
User Query
    │
    ▼
Vector Retriever (FAISS)
    │
    ▼
Retrieved Documents
    │
    ▼
LLM Retrieval Evaluator
    │
    ├── Correct
    │     └─ Context Refinement → Generate Answer
    │
    ├── Ambiguous
    │     └─ Query Rewrite → Web Search → Context Refinement
    │
    └── Incorrect
          └─ Web Search → Context Refinement

This creates a self-correcting RAG system.

Key Features
Baseline RAG

PDF ingestion

Chunking and embedding

FAISS vector database

Retrieval augmented generation

Corrective RAG (CRAG)

Implemented components from the research paper:

Retrieval Evaluator

LLM classifies retrieved documents into:

Label	Meaning
Correct	Relevant information present
Ambiguous	Partial relevance
Incorrect	Irrelevant documents
Query Rewriting

Ambiguous queries are rewritten before external search.

Example:

Original Query:
"What does CRAG improve?"

Rewritten Query:
"How does Corrective Retrieval Augmented Generation reduce hallucinations?"
External Knowledge Retrieval

If retrieval fails:

Web search using Tavily

Additional knowledge sources retrieved

Knowledge Refinement

Refinement process:

Sentence level filtering

Removal of irrelevant context

Creation of clean context for LLM

Project Architecture
User Query
     │
     ▼
Retriever (FAISS)
     │
     ▼
Document Evaluator (LLM)
     │
     ├─ Correct → Context Refinement → Answer Generation
     │
     ├─ Ambiguous → Query Rewrite → Web Search → Refinement
     │
     └─ Incorrect → Web Search → Refinement
Tech Stack
Component	Technology
LLM	OpenAI GPT
Orchestration	LangGraph
Retrieval	FAISS
Framework	LangChain
Web Search	Tavily
Language	Python
Repository Structure
corrective-rag/
│
├── notebooks/
│   ├── 1_basic_rag.ipynb
│   └── 6_ambiguous.ipynb
│
├── src/
│   ├── retriever.py
│   ├── evaluator.py
│   ├── query_rewrite.py
│   ├── web_search.py
│   └── generator.py
│
├── demo/
│   └── streamlit_app.py
│
├── data/
│   └── sample_documents
│
├── requirements.txt
├── .env.example
└── README.md
Installation

Clone repository

git clone https://github.com/YOUR_USERNAME/corrective-rag
cd corrective-rag

Install dependencies

pip install -r requirements.txt
Environment Variables

Create .env file

OPENAI_API_KEY=your_api_key
TAVILY_API_KEY=your_api_key
Running the Project

Run notebooks:

notebooks/1_basic_rag.ipynb

or

notebooks/6_ambiguous.ipynb

Example query:

What are the key contributions of the CRAG paper?
Demo UI (Streamlit)

This project includes a lightweight Streamlit demo.

Run:

streamlit run demo/streamlit_app.py

Interface features:

User query input

Retrieval evaluation output

Web search trigger visualization

Final answer with citations

Evaluation

To evaluate improvements over standard RAG:

Dataset:

~50 evaluation queries

Document QA benchmark

Metrics used:

Metric	Description
Faithfulness	Answer grounded in context
Correctness	Answer matches ground truth
Hallucination rate	Incorrect facts generated
Retrieval quality	Relevance of retrieved chunks
Example Comparison
Model	Hallucination Rate
Baseline RAG	Higher
Corrective RAG	Lower

CRAG improves reliability by correcting retrieval before generation.

Example Output

Baseline RAG:

Answer generated using retrieved chunks.
Context may contain irrelevant information.

Corrective RAG:

Retrieval verdict: AMBIGUOUS
Query rewritten
Web search triggered
Context refined
Grounded answer generated
Future Improvements

Planned extensions:

Hybrid retrieval (BM25 + vector)

RAGAS evaluation metrics

multi-agent retrieval pipelines

multi-document QA benchmarks

knowledge graph integration

References

Shi-Qi Yan et al.

Corrective Retrieval Augmented Generation
https://arxiv.org/pdf/2401.15884

License

MIT License

Summary

This project demonstrates:

Implementation of research-grade RAG architecture

Hallucination mitigation techniques

LLM-based retrieval evaluation

Dynamic knowledge correction pipelines

This type of system is used in modern production LLM applications and AI agents.
