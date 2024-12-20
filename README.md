# RAG Model for Electric Vehicle Automobile Assistance

This project demonstrates a Retrieval Augmented Generation (RAG) pipeline for answering questions about the Tata Tiago EV owner's manual and sales data.  It leverages LLMs, vector databases, and the RAGAS framework for evaluation.  Additionally, it includes a Text-to-SQL component for querying sales data.

## Data Sources

* **Tata Tiago EV Owner's Manual (PDF):** [https://ev.tatamotors.com/content/dam/tml/ev/pdf/owners-manual/tiago-ev-owner-manual.pdf](https://ev.tatamotors.com/content/dam/tml/ev/pdf/owners-manual/tiago-ev-owner-manual.pdf)
* **Region-wise Retail Sales Data (CSV):**  RetailFYPV.csv (Assumed to be present in the same directory as the notebook)


## Project Setup

1.  **Install Dependencies:** The project uses several Python libraries.  Install them using the `requirements.txt` file:
    ```bash
    pip install -r requirements.txt
    ```

2. **Ollama:** The project utilizes Ollama for the LLM. Ensure Ollama is running locally and accessible at the specified URL. You might need to download a model first:

    ```bash
    # Example using Llama3.2
    ./ollama run llama3.2
    ```
   
3. **API Keys:**  Set your OpenAI API key as an environment variable:
    ```bash
    export OPENAI_API_KEY="YOUR_OPENAI_API_KEY"
    ```

4. **Data Files:** Place the `RetailFYPV.csv` file in the same directory as the notebook.


## Project Structure

The code is structured as a Jupyter Notebook or Colab notebook.  The key components include:

*   **Data Loading and Preprocessing:** Downloads the PDF manual, splits it into chunks, and creates embeddings using Ollama embeddings.
*   **Vector Database:** Stores the embeddings in a Chroma vector database.
*   **RAG Pipeline:** Implements a RAG pipeline combining the retriever, a prompt template, the LLM, and an output parser.
*   **Evaluation:** Evaluates the RAG pipeline using RAGAS metrics (faithfulness, answer relevancy, context recall, context precision).
*   **Text-to-SQL:** Converts natural language queries about the sales data into executable SQL queries using an LLM.


## Usage

1.  Run the Jupyter Notebook/Google Colab notebook.
2.  The notebook will download the PDF, process it, and create a vector database.
3.  The RAG pipeline will be tested with sample questions, and the results will be evaluated using RAGAS.
4. The Text-to-SQL component will then be demonstrated with example queries and outputs.


## Evaluation Metrics

The RAG pipeline is evaluated using the following RAGAS metrics:

*   **Faithfulness:** Measures factual accuracy of generated answer with respect to retrieved context.
*   **Answer Relevancy:** Measures how well answer is relevant to the query.
*   **Context Recall:** Measures how much of the relevant context was retrieved.
*   **Context Precision:** Measures if retrieved context is relevant to the query.

The results are saved to a CSV file (`results.csv`) and displayed in the notebook.

## Text-to-SQL Queries

The following sample queries are used to demonstrate the Text-to-SQL functionality:

*   List all Retail sales for the 'Altroz XE 1.2 P' in the fiscal year 2024-25.
*   Show the total Retail sales for each PPL grouped by LOB for April 2024.
*   Which PL had the highest Retail sales in 2024-25?
*   Display Retail sales for all PPLs under the BU 'TMPC'.
*   Find the average Retail sales per month for the LOB 'Cars'.

The generated SQL queries are executed using pandasql, and the results are displayed in the notebook
