# Automated GitHub PR Code Reviews with Repo Context RAG & Vector Store Builder

## Overview

This n8n automation package includes two workflows designed to support more context-aware and informed GitHub pull request (PR) code reviews by integrating repository-specific information through a Retrieval-Augmented Generation (RAG) system.

---

## Vector Store Builder Workflow

Creates and updates a Qdrant vector store containing embeddings from repository documents including architecture guides, coding standards, contribution guidelines, and other essential project files. This vector store acts as a structured knowledge base for AI-assisted code reviews.

---

## AI-Powered PR Review Workflow

Automatically processes open PRs by analyzing code changes with the context retrieved from the vector store. An Ollama language model generates structured review comments that reference project-specific rules and best practices. Reviews are posted as GitHub comments and can optionally be sent by email.

---

## What This Package Does

- Incorporates repository context into AI code reviews, enabling feedback aligned with project-specific standards and guidelines.
- Automates fetching of PRs, commit diffs, and changed files, providing the AI with detailed input.
- Uses semantic search over repo documents to inform review feedback, reducing generic or irrelevant comments.
- Produces detailed, actionable reviews with specific file and line references, severity markings, and clear recommendations.
- Supports automated delivery of review results via GitHub comments and optional email notifications.

---

## Features

### Vector Store Builder Workflow

- Connects to GitHub to retrieve repository source code and documentation files.
- Generates vector embeddings using an Ollama embedding model.
- Stores and manages embeddings in a Qdrant vector database.
- Keeps repository context synchronized for accurate, up-to-date AI queries.

### AI-Powered PR Review Workflow

- Triggered on a schedule or manually, obtains and analyzes latest PRs and associated commit diffs.
- Aggregates file and code changes for input to the AI reviewer.
- Retrieves relevant repository context via Qdrant to inform the review.
- Generates structured, markdown-formatted reviews including:
  - Clear summaries of PR intent
  - Bulleted lists of key code changes
  - In-depth review comments with file paths, line numbers, severity icons, and detailed suggestions
  - Additional recommendations around security, error handling, testing, and documentation
- Automates posting of reviews as comments on GitHub PRs.
- Optionally sends review summaries via email.

---

## Retrieval-Augmented Generation (RAG) System

- The AI model dynamically consults the vector store to ground its responses in actual project documentation and codebase context.
- Enables the AI to check compliance with enforced coding guidelines, architectural patterns, and testing standards.
- Helps avoid irrelevant or generic feedback by tying recommendations to specific repository rules.
- Keeps AI reviews aligned with the current state of the repository as the vector store is regularly updated.

---

## Workflow Components Summary

| Workflow               | Key Nodes & Roles                                      |
|------------------------|-------------------------------------------------------|
| Vector Store Builder   | GitHub API, Ollama Embeddings, Qdrant Storage, Control Logic |
| AI PR Review           | Scheduler, GitHub PR API, Diff Aggregator, Vector Retrieval, Ollama LLM, Markdown Formatter, Email & HTTP nodes |

---

## Environment & Compatibility

This automation has been built and tested primarily on a local Mac environment using the [n8n Self-hosted AI Starter Kit](https://github.com/n8n-io/self-hosted-ai-starter-kit). It leverages embedded models and a local Ollama LLM with Qdrant vector storage for full privacy and control.

This solution can be adapted to work with external embedding models and LLMs such as OpenAI’s ChatGPT and Anthropic’s Claude, enabling flexible integration based on your infrastructure and needs.

For more details and an easy-to-follow setup guide, check out the blog post:  
[Automating Context-Aware GitHub PR Code Reviews with n8n, RAG, LLMs & Vector Store](https://medium.com/@skalrd/automating-context-aware-github-pr-code-reviews-with-n8n-rag-llms-vector-store-838cbd6c2776)

---

## Getting Started

1. Configure credentials for GitHub, Qdrant, Ollama (LLM and embeddings), and optionally SMTP for emails.
2. Run the Vector Store Builder periodically or after repository updates to refresh the context data.
3. Enable and schedule the AI PR Review workflow to run at desired intervals.
4. Reviews will be posted automatically as comments on GitHub PRs, with optional email summaries.
5. Customize thresholds, triggers, or output formatting as needed for your project’s workflow.

---

## Sample Review Output Format

**Introductory Summary**  
The PR implements user profile management and bulk user registration features with new endpoints and extended notification support.

**Key Changes**  
- Added `GET/PUT /api/v1/users/{id}` endpoints.  
- Introduced bulk user registration logic.  
- Enhanced multi-channel notifications (email/SMS).

**Review Comments**  
**❌ Direct Repository Access in Controller (UserProfileController.java:55)**  
Bypasses service layer contrary to architecture pattern.  
Recommendation: Use the service layer for data operations.

**⚠️ Mixed Indentation (UserProfileServiceImpl.java:65)**  
Inconsistent use of tabs and spaces.  
Recommendation: Standardize to 4 spaces per project convention.

...additional comments...

**Additional Suggestions and Observations**  
- Ensure password hashing is implemented before production.  
- Add detailed logging for notification failures.  
- Expand testing to cover edge cases.

---

## Keywords & Tags

Code Review, GitHub, Vector Store, Qdrant, Ollama, AI, Retrieval-Augmented Generation, RAG, Automation, Developer Productivity, PR Analysis, Markdown Reviews, Email Notifications

