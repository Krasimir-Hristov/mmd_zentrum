---
name: AI Agent Integration Skill
description: Roadmap and patterns for implementing the AI capabilities.
---

# AI Agent Integration Skill

## Core Vision

The AI Agent is a "First-Class Citizen" in MakroFlow. It observes, assists, and automates.

## Implementation Pattern (RAG)

### 1. Vector Embeddings

- **Docs/Projects**: When created, generate embedding (OpenAI `text-embedding-3-small`).
- **Storage**: Store in `pgvector` column in Postgres.

### 2. Context Retrieval

- **Query**: "What is the deadline for Project X?"
- **Search**: Cosine similarity search in `pgvector`.
- **Prompt**: "You are a PM assistant. Answer based on this context: {context}".

## Frontend Integration

- **Streaming**: Use Vercel AI SDK or `useChat` for streaming responses.
- **UI**: Floating Sidebar or dedicated `/chat` route.
- **Tools**: Give the AI tools to fetch data live (`get_project_status(id)`).

## Future Automation

- **Background Jobs**: AI agents running on cron to check stale tasks.
- **Drafting**: AI pre-fills Description fields based on Project Title.
