# README

## Project Overview

This project is a Document Chatbot that uses Streamlit for the user interface and the Ollama model for question-answering tasks. The chatbot ingests a document and then answers questions based on the information in the document.

## Prerequisites

- Python 3.9 or higher
- Streamlit 1.31.1 or higher
- Ollama model from the Langchain library
- Mistral model

## Installation

1. Clone the repository:
    ```
    git clone https://github.com/timpara/docuchat.git
    ```
2. Navigate to the project directory:
    ```
    cd docuchat
    ```
3. Install the dependencies:
    ```
    poetry install
    ```
4. Install the Ollama model:
    ```
    ollama pull mistral
    ```

## Usage

1. Start the Streamlit server:
    ```
    streamlit run app.py
    ```
2. Open your web browser and go to `http://localhost:8501`.
3. Upload a document using the file uploader. The supported file types are PDF, Markdown (md), Text (txt), Word (docx, doc).
4. After the document is ingested, you can ask questions in the text input field labeled "Message". The chatbot will answer based on the information in the uploaded document.

## How it Works

The chatbot uses the Ollama model for question-answering tasks. When a document is uploaded, the `ChatDocument` class ingests the document, splits it into chunks, and stores it in a vector store. The `ChatDocument` class also sets up a retriever and a chat model chain.
When a question is asked, the `ChatDocument` class uses the retriever to find relevant context in the vector store. The context and the question are then passed to the chat model chain, which generates an answer.

The Streamlit interface provides a user-friendly way to interact with the chatbot. It allows you to upload documents, ask questions, and view the chatbot's answers.

The Document Chatbot works in the following way:

1. **Ingestion**: When a document is uploaded, the `ChatDocument` class ingests the document. This is done in the `ingest` method. The document is loaded using the `UnstructuredMarkdownLoader` class from the `langchain_community.document_loaders` module. The document is then split into chunks using the `MarkdownTextSplitter` class from the `langchain.text_splitter` module. These chunks are then filtered to remove complex metadata.

2. **Vector Store Creation**: The chunks are then used to create a vector store using the `Chroma` class from the `langchain.vectorstores` module. The `Chroma` class uses the `FastEmbedEmbeddings` class from the `langchain.embeddings` module to create embeddings for the chunks. These embeddings are then stored in the vector store.

3. **Retriever Setup**: The vector store is then used to set up a retriever. The retriever is used to find relevant context in the vector store when a question is asked. The retriever is set up to return the top 3 results that have a similarity score of at least 0.1.

4. **Chat Model Chain Setup**: A chat model chain is then set up. The chat model chain is a sequence of operations that are performed to generate an answer. The chat model chain consists of the retriever, a prompt, the Ollama model, and an output parser. The retriever provides the context, the prompt formats the context and the question, the Ollama model generates an answer, and the output parser formats the answer.

5. **Question Answering**: When a question is asked, the `ChatDocument` class uses the chat model chain to generate an answer. The `ChatDocument` class uses the retriever to find relevant context in the vector store. The context and the question are then passed to the chat model chain, which generates an answer.

The Streamlit interface provides a user-friendly way to interact with the chatbot. It allows you to upload documents, ask questions, and view the chatbot's answers. The interface is defined in the `app.py` file. The interface uses the `streamlit` and `streamlit_chat` modules to create a web page with a file uploader and a chat interface. The file uploader is used to upload documents, and the chat interface is used to ask questions and view answers.