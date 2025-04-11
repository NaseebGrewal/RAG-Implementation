# Data Pipeline Architecture

This document outlines the data pipeline architecture for processing organization data, generating document embeddings, and storing these embeddings in an index for fast retrieval. The pipeline follows a sequential data flow as described below:

1. **File Path**  
   The pipeline begins by reading raw data from a specified file path.

2. **Information Extraction via Regular Expression**  
   A regular expression is applied to the raw file content to extract relevant information (e.g., document ID, title, and description) based on a defined pattern.

3. **Document Conversion and Chunking**  
   - The extracted text is converted into structured documents.
   - For larger text blocks, the text is split into smaller, manageable chunks to preserve semantic context while ensuring processing efficiency.

4. **Embedding Generation**  
   The resulting documents or document chunks are fed into an embedding function that leverages a pre-trained SentenceTransformer model to create vector embeddings.

5. **Indexing**  
   Finally, the generated embeddings are saved into a FAISS index, allowing for efficient similarity searches and fast retrieval during inference.

---

# Data Pipeline Architecture

This section outlines the sequential data flow in our pipeline for processing organization data. The pipeline efficiently handles raw inputs by extracting data, processing documents, creating embeddings with a SentenceTransformer, and saving these embeddings in a FAISS index for fast retrieval.

Below is the data flow diagram representing this pipeline:
### 4. **ASCII Art**
   For simple diagrams, you can use plain text or ASCII art directly in your Markdown file:

   ```plaintext
   [Raw Data File Path] --> [Regex Extraction] --> [Convert to Documents]
                                |
                                v
                     [Large Document?]
                      /       \
                    Yes       No
                     |         |
          [Split into Chunks] [Retain as Documents]
                                |
                                v
                      [Embedding Function]
                                |
                                v
                 [Save Embeddings to FAISS Index]
   ```
---

### 5. **Markdown Tables**

   ```markdown
   | Step                     | Description                          |
   |--------------------------|--------------------------------------|
   | Raw Data File Path       | Read raw data from a file.          |
   | Regex Extraction         | Extract information using regex.    |
   | Convert to Documents     | Convert extracted text to documents.|
   | Large Document?          | Check if the document is large.     |
   | Split into Chunks        | Split large documents into chunks.  |
   | Embedding Function       | Generate embeddings for documents.  |
   | Save to FAISS Index      | Save embeddings to FAISS index.     |
   ```

This diagram  demonstrates the following steps:
- **Raw Data File Path:** The pipeline begins by reading the raw data from a specified file.
- **Regular Expression Extraction:** A regular expression extracts valuable information (e.g., document IDs, titles, descriptions).
- **Document Conversion and Chunking:**  
  - If a document is large, it is split into smaller, manageable chunks.
  - Otherwise, it is processed as a whole.
- **Embedding Generation:** Documents or chunks are then encoded into vector embeddings.
- **Indexing:** Finally, the embeddings are saved into a FAISS index to support efficient similarity search during retrieval.

This scalable and efficient architecture is designed for robust document ingestion, embedding, and retrieval in production-level deployments.