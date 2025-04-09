# Retrieval-Augmented Generation (RAG) System

This project implements a simple Retrieval-Augmented Generation (RAG) system with different prompt techniques.

---

## Project Overview

The system performs the following steps:
- **Data Indexing:** Loads and indexes a dataset of fictional financial organizations.
- **Embedding:** Uses a pre-trained SentenceTransformer model to generate document embeddings.
- **Similarity Search:** Employs FAISS to perform vector similarity search.
- **Prompt Construction:** Builds a query prompt using the top-k retrieved documents.
- **Response Generation:** Utilizes Mistral (via Hugging Face API) to generate a human-like answer.

---

## File Structure

```
Hawk-Submission/
├── Data/
|     └──dataset.txt    
├── README.md    
├── Problem_statement.md
├── submission_rag_assignment.ipynb      # Main notebook containing the implementation
├── requirements.txt                     # Python dependencies list
└── .env                                 # Environment variables configuration NOTE: faiss-cpu library only works for Mac and Linux system
```

---

## Technologies Used

- Python 3.13
- [FAISS](https://github.com/facebookresearch/faiss)
- [SentenceTransformers](https://www.sbert.net/)
- [Hugging Face Mistral API](https://huggingface.co/inference-api)
- [OpenAI API](https://platform.openai.com/docs/overview)
- dotenv for environment management
- NumPy for vector operations

---

## Getting Started

1. **Clone this Repository:**
    ```bash
    git clone https://github.com/NaseebGrewal/RAG-Implementation.git
    cd RAG-Implementation
    ```

2. **Install Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3. **Configure Environment Variables:**
   Create a `.env` file in the project root with the following contents:
    ```
    HUGGINGFACE_API_TOKEN=your_token_here
    FILE_PATH=path_to_your_data.txt
    OPENAI_API_KEY=your_openai_api_key
    ```

4. **Run the Notebook:**
   Open `submission_rag_assignment.ipynb` in Jupyter Notebook or VS Code’s Jupyter extension and run all cells.

---

## Example Query

For example, you can test the system with the query:
```
"Tell me about Celestial Capital Groups?"
```

The process will:
- Retrieve relevant organization profiles.
- Build an informative prompt.
- Generate a detailed, human-like response using the Mistral model.

---

## Author Notes

This implementation is modular and designed to be easily extended. Future improvements could include:
- Integrating alternative embedding models.
- Enhancing prompt strategies.
- Expanding the dataset or improving the data indexing.

---

## License

This project is for educational use only.
