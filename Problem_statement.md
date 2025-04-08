# Take Home Assignment

## Objective

In today’s financial landscape, detecting suspicious patterns among organizations is critical to combat financial crime. In this assignment, you will build a simple Retrieval-Augmented Generation (RAG) system that:

- Indexes a provided dataset of fictional organization descriptions.  
- Retrieves the most relevant organizations based on a natural language query.  
- Constructs an effective prompt by integrating the retrieved context.  
- Uses a large language model (LLM) to generate a coherent answer addressing the query.

---

## Problem Statement

Financial institutions and regulatory bodies must quickly identify organizations that may pose compliance risks or be involved in financial crime. You are provided with a dataset containing 12 fictional organization descriptions. Each document includes a brief profile that outlines key details.

Your task is to build a system that, when given a query (for example, _"Which organizations show signs of potential money laundering through complex structures?"_), retrieves the most relevant organization profiles and uses them as context to generate an informed answer via an LLM.

---

## Assignment Deliverables

### Implementation

- Develop a Python script or Jupyter Notebook that:
  - Reads and indexes the provided organization descriptions.  
  - Creates vector embeddings for each document (using a pre-trained embedding model or API).  
  - Implements a retrieval mechanism to find relevant documents based on a query.  
  - Constructs a prompt that incorporates the retrieved context.  
  - Uses the prompt to query an LLM and generate an answer.

---

### Documentation

- Write a short report (1–2 pages) explaining:
  - Your approach to document ingestion, indexing, and retrieval.  
  - The design of your prompt and any experiments you conducted with prompt variations.  
  - Observations on how prompt modifications impacted the LLM’s responses and the overall system performance.

---

### Testing

- Provide at least one example query along with the system’s output, highlighting the retrieval step and the final generated answer.

---

## Time Expectation

The task is designed to be completed within **2–4 hours**.

---

## Notes

Of course you can use open source libraries as you see fit to complete the task.
