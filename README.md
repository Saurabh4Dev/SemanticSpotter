# MrHelpMateAI


# Project Name
> Semantic spotter project - RAG Q&A System for Insurance Policies using LangChain 


## General Information

In the insurance industry, life insurance policy documents are often lengthy and complex involving legal terminology. This makes it difficult for customers\policyholders to quickly find answers to specific questions such as eligibility, exclusions, claim procedures, or grace periods. Answers to user queries exist in the documents, but are often buried across different sections and may vary between policy types. Traditional search systems struggle to interpret natural language queries.
Semantic Spotter project aims to implement such a system for life insurance documents. By leveraging embedding models, vector databases like ChromaDB, cross-encoder reranking, LangChain framework and OpenAI’s GPT models, the system delivers accurate, context-aware answers to user queries. Additionally, it implements a caching mechanism to optimize repeated query performance, improving both response speed and cost efficiency.

## Problem Statement
The goal of the project is to build a robust generative search system capable of effectively and accurately answering questions from a bunch of policy documents using LangChain framework.

## Objectives

To build a Retrieval-Augmented Generation (RAG) system that:
•	Accepts user questions in natural language.
•	Retrieves relevant sections from one or more insurance policy documents.
•	Generates an accurate, grounded answer using only the retrieved content.

## Why LangChain?
LangChain is a framework that simplifies the development of LLM applications LangChain offers a suite of tools, components, and interfaces that simplify the construction of LLM-centric applications. LangChain enables developers to build applications that can generate creative and contextually relevant content LangChain provides an LLM class designed for interfacing with various language model providers, such as OpenAI, Cohere, and Hugging Face.
LangChain is an open-source framework that makes it easier to build powerful and personalizeable applications with LLMs relevant to user’s interests and needs. It connects to external systems to access information required to solve complex problems. It provides abstractions for most of the functionalities needed for building an LLM application and also has integrations that can readily read and write data, reducing the development speed of the application. LangChains's framework allows for building applications that are agnostic to the underlying language model. With its ever expanding support for various LLMs, LangChain offers a unique value proposition to build applications and iterate continuously.
LangChain framework consists of the following:
•	Components: LangChain provides modular abstractions for the components necessary to work with language models. LangChain also has collections of implementations for all these abstractions. The components are designed to be easy to use, regardless of whether you are using the rest of the LangChain framework or not.
•	Use-Case Specific Chains: Chains can be thought of as assembling these components in particular ways in order to best accomplish a particular use case. These are intended to be a higher level interface through which people can easily get started with a specific use case. These chains are also designed to be customizable.
The LangChain framework revolves around the following building blocks:
•	Model I/O: Interface with language models (LLMs & Chat Models, Prompts, Output Parsers).
•	Retrieval: Interface with application-specific data (Document loaders, Document transformers, Text embedding models, Vector stores, Retrievers).
•	Chains: Construct sequences/chains of LLM calls.
•	Memory: Persist application state between runs of a chain.
•	Agents: Let chains choose which tools to use given high-level directives.
•	Callbacks: Log and stream intermediate steps of any chain.


## Design
The RAG-based semantic retrieval system is designed to answer questions from PDF documents using LangChain. The system is composed of multiple modular components that work together in a pipeline to process, retrieve, and generate responses from document content.
1.	PDF Reading & Processing
PyPDFDirectoryLoader from LangChain’s document loaders module is used to load\read recursively all PDF files from a specified directory. Each document is loaded with metadata (like file path and page number) which is essential for traceability and citation.
2.	Document Chunking
After loading, documents are split into smaller units (chunks) using RecursiveCharacterTextSplitter. This splitter breaks down the text intelligently by attempting to preserve semantic boundaries. It tries to split on paragraph (\n\n), line (\n), word ( ), or character ("") levels—only when absolutely necessary. This avoids breaking up clauses or definitions mid-sentence, which improves embedding quality and search recall.
3.	Embedding Generation
We use OpenAIEmbeddings from LangChain to convert each chunk of text into a dense vector representation. These embeddings encode semantic meaning and allow similarity comparison between a query and document chunk.
4.	Storing Embeddings in ChromaDB
The generated embeddings are stored in ChromaDB, a lightweight, local vector database integrated with LangChain. To boost performance and avoid redundant computation, embeddings are wrapped using CacheBackedEmbeddings, allowing you to cache embeddings on disk.
5.	Re-Ranking with Cross-Encoder
To further improve relevance a re-ranker after retrieval is applied. HuggingFaceCrossEncoder is used with the model BAAI/bge-reranker-base. This model evaluates each (query, passage) pair and reorders the retrieved chunks based on semantic relevance scores.It ensures that only the most contextually appropriate ones are passed to the language model.
6.	RAG Chain with LangChainHub Prompt
Connects everything using a LangChain RAG Chain, where:
6.1	The top-ranked context chunks are formatted with a RAG-specific prompt.
6.2	Pull the prompt from LangChainHub using the template: rlm/rag-prompt.
6.3	The formatted prompt and query are passed to an LLM to generate a grounded answer.

 
## Tools and Technologies
- Python 3.10.4
- Jupyter notebook
- Langchanin, LLM(OpenAI GPT, Huggingface)
- ChromaDB(Vector DB)

<!-- As the libraries versions keep on changing, it is recommended to mention the version of library used in this project -->

## Conclusions
Developed a solution to query PDF documents using Langchain framework for RAG implementation.


## Contact
Created by Saurabh Pandey(@Saurabh4Dev) - feel free to contact me!
