# Traditional Retrieval-Augmented Generation (RAG)
This project demonstrates a foundational implementation of a Traditional Retrieval-Augmented Generation (RAG) system. It's designed to be beginner-friendly, focusing on the core concepts of RAG using an in-memory vector database for simplicity. The goal is to show how Large Language Models (LLMs) can be enhanced by retrieving relevant information from a custom knowledge base before generating responses.

## Project Description
Large Language Models are incredibly powerful, but their knowledge is limited to their training data and can become outdated. They also sometimes "hallucinate" or provide incorrect information. RAG addresses these challenges by allowing an LLM to access and incorporate external, up-to-date information.

This project sets up a basic RAG pipeline where:

Your custom documents are processed and stored in a searchable format.

When a query comes in, the system retrieves the most relevant pieces of information from your documents.

These retrieved pieces are then fed to an LLM along with the original query, enabling the LLM to generate more accurate, grounded, and context-aware answers.

It's a great starting point for understanding how to ground LLMs with your own data!

## Technologies Used
Python: The primary programming language for the project.

LangChain: A powerful framework used to streamline the development of LLM applications, handling components like document loading, text splitting, embeddings, and chaining.

FAISS (Facebook AI Similarity Search): An open-source library for efficient similarity search. In this project, it's used as an in-memory vector database to store and quickly search document embeddings. Being in-memory, it's simple to set up for local development without needing external database services.

OpenAI Embeddings: Used to convert text (both your documents and user queries) into numerical vector representations (embeddings).

ChatOpenAI: The Large Language Model (LLM) from OpenAI used for generating responses.

## How It Works
The Traditional RAG pipeline in this project follows two main phases:

**Phase 1**: Indexing (Building the Knowledge Base)
Document Loading: Your raw documents (e.g., text files, PDFs) are loaded into the system.

Text Splitting (Chunking): Large documents are broken down into smaller, manageable chunks. This is crucial because LLMs have a limited context window.

Embedding Generation: Each text chunk is converted into a high-dimensional numerical vector (an embedding) using OpenAIEmbeddings. Text chunks with similar meanings will have similar vectors.

FAISS Indexing: These embeddings are then stored in a FAISS index. FAISS is optimized for quickly finding the "nearest neighbors" (most similar vectors) to a given query vector.

**Phase 2**: Retrieval & Generation (Answering Queries)
User Query: A user asks a question.

Query Embedding: The user's query is also converted into an embedding using the same OpenAIEmbeddings model.

FAISS Search: The query embedding is used to search the FAISS index to find the most relevant document chunks (i.e., the embeddings closest to the query embedding).

Context Augmentation: The retrieved text chunks are combined with the original user query to create a rich, augmented prompt.

LLM Generation: This augmented prompt is sent to ChatOpenAI. The LLM then generates an answer, leveraging both its pre-trained knowledge and the specific, relevant context provided by the retrieved chunks, leading to a more accurate and grounded response.

