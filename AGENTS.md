# DeepWiki-Open Project Summary

## Overview
DeepWiki-Open is an automated documentation and knowledge base generation tool for software repositories. It leverages AI to analyze codebases (GitHub, GitLab, BitBucket) and constructs interactive wikis complete with documentation, architectural diagrams, and navigation structures.

## Core Capabilities
*   **Instant Wiki Generation:** transform repositories into structured wikis automatically.
*   **Code Analysis:** AI-powered parsing of code structure and dependencies.
*   **Visualizations:** Auto-generation of Mermaid diagrams for architecture and data flow.
*   **Interactive "Ask" Interface:** A RAG (Retrieval-Augmented Generation) powered chat interface allowing users to query the codebase using natural language.
*   **Deep Research:** Multi-turn investigative capabilities for complex topics within the repo.
*   **Privacy & Flexibility:** Supports private repositories and multiple AI providers.

## Technology Stack

### Frontend
*   **Framework:** Next.js 15 (React 19)
*   **Styling:** Tailwind CSS 4
*   **Visualization:** Mermaid.js, React Syntax Highlighter
*   **Language:** TypeScript

### Backend (API)
*   **Framework:** Python (FastAPI)
*   **Dependency Management:** Poetry
*   **Core Libraries:** `pydantic`, `fastapi`, `uvicorn`

### AI & LLM Infrastructure
*   **Providers:** Supports Google Gemini, OpenAI, Azure OpenAI, OpenRouter, and local Ollama models.
*   **Embeddings:** Configurable options including OpenAI, Google AI, and local Ollama embeddings.
*   **Vector Search:** Utilizes FAISS for efficient similarity search.
