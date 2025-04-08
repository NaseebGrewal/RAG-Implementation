
# Short Report: Document Ingestion, Indexing, Retrieval, and Prompt Design

## 🔍 Document Ingestion, Indexing, and Retrieval

The system is built around a simple **Retrieval-Augmented Generation (RAG)** pipeline for identifying organizations with potential financial crime risks.

### 1. Document Ingestion:
- The dataset is read from a plain text file containing fictional organization profiles.
- A regular expression pattern is used to extract document IDs, titles, and descriptions.

### 2. Vectorization & Embedding:
- A SentenceTransformer model (`BAAI/bge-small-en-v1.5`) is used to embed each document.
- Texts are concatenated into the format `"Title: Description"` and then embedded into dense vectors.

### 3. Indexing using FAISS:
- All embeddings are added to a FAISS `IndexFlatL2` index for efficient similarity search.
- Each document’s metadata is stored in a `id_to_docs` dictionary, keyed by the FAISS index position.

### 4. Query Retrieval:
- The same SentenceTransformer model is used to embed the user query.
- FAISS returns the top-k closest documents based on vector similarity.
- The titles and descriptions of these documents are formatted into context for the LLM.

---

## Prompt Design & Experiments

The final prompt sent to the LLM is constructed in a clear instruction-following format:

```
<s>[INST] Your task is to analyse the question based on the context and provide a suitable answer.

Context:
<top-k document info>

Question: <query>

Answer: [/INST]
```

- This format follows the **ChatML-style** used by Mistral-Instruct models.
- Experiments showed that wrapping context and instructions explicitly improved the clarity and structure of generated answers.
- The use of `return_full_text=False` in the Hugging Face API ensured that only the generated answer was returned, keeping the response clean.

---

## Observations on Prompt Impact

- **Structured prompts** like `[INST]...[/INST]` helped Mistral understand and follow instructions better.
- **Vague or minimal prompts** often led to generic answers with hallucinated content.
- Adding context in a bullet or numbered format didn’t help significantly over the current structure.
- Using `max_new_tokens=512` provided sufficient response length without overwhelming output.

---

# Testing Example

### Query:
> Tell me about Celestial Capital Groups?

### Retrieved Context:
```
Rank 1:
Title: Cascade Capital Management
Description: Cascade Capital Management, a venture capital firm specializing in tech investments, has grown rapidly but relies on a complex network of subsidiary shell companies. This structure has attracted regulatory scrutiny regarding transparency and compliance.
Distance: 0.2569

Rank 2:
Title: Gemini Asset Management
Description: Serving high-net-worth clients in Asia, Gemini Asset Management has recently been spotlighted for unusually high commissions and inconsistent portfolio reporting. These anomalies have sparked concerns over potential money laundering and fraudulent practices.
Distance: 0.7213

Rank 3:
Title: Blue Horizon Investments
Description: Based in London, Blue Horizon Investments is known for its innovative portfolio strategies. However, irregular transaction patterns and rapid, unexplained fund movements have raised concerns about possible insider trading and manipulation.
Distance: 0.7599

Rank 4:
Title: Kepler Financial Innovations
Description: Kepler Financial Innovations is renowned for its ethical practices and state-of-the-art risk management. With a focus on transparency and regulatory compliance, the firm has built a reputation as a trusted player in the financial market.
Distance: 0.7645

Rank 5:
Title: Helix Fintech Solutions
Description: Helix Fintech Solutions is a rapidly growing startup in the financial technology space. Its strategy of partnering with numerous unregulated advisors has resulted in a patchwork of compliance practices, prompting internal reviews for potential fraud and mismanagement of client funds.
Distance: 0.8210
```

### Final Prompt:
```
<s>[INST] Your task is to analyse the question based on the context and provide a suitable answer.

Context:
Title: Celestial Capital Groups
Description: A private equity firm with investments in aerospace and defense. Several of its portfolio companies have been flagged for opaque ownership structures and overseas transactions.

Title: Zenith Finance
Description: A fintech startup offering cross-border payment services. Reports indicate high transaction volume with minimal regulatory oversight.

Question: Tell me about Celestial Capital Groups?

Answer: [/INST]
```

### Generated Answer:
> Celestial Capital Groups is a private equity firm involved in aerospace and defense sectors. It has raised compliance concerns due to its portfolio companies being linked with opaque ownership and overseas financial transactions, which could be indicative of money laundering or regulatory evasion.
