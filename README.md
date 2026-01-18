# MakroFlow (MMD_Zentrum)

## Project Vision

**MakroFlow** is a specialized internal project and document management system designed for **Makro Medien Dienst**. It serves as a streamlined, secure, and fast alternative to complex Agile tools, focusing on simplicity and efficiency.

## Core Functionality

### Centralized File Vault

A global database for PDF and media files. Files are uploaded once and can be linked to multiple projects, ensuring a single source of truth (SSOT).

### Simplified Project Management

- **Project Structure**: Projects have a fixed "Owner" (immutable).
- **Team Management**: Easy team onboarding.
- **Deadlines**: Clear timeline management.

### Task Tracking (Agile-Lite)

Break down projects into independent tasks with simple statuses:

- **Pending**
- **In Progress**
- **Complete**

### Role-Based Access Control (RBAC)

- **Owner**: Full control and immunity.
- **Admin**: User and project management.
- **Worker**: Task execution and file handling.
- **Viewer**: Read-only access.

### Print & Search

- **Instant Search**: Rapid retrieval of documents.
- **Direct Print**: Integration for printing documents directly from the interface.

## Architectural Principles & Best Practices

To ensure scalability and future AI integration:

1.  **Design-First**: UI components are built after defining data logic.
2.  **Atomic Design**: Use small, reusable UI components (Buttons, Badges, Inputs).
3.  **Row Level Security (RLS)**: Security is enforced at the database level (Supabase), not just the frontend.
4.  **Modular Routing**: Backend routers are separated by domain (`/users`, `/projects`, `/files`).
5.  **Optimistic Updates**: The Frontend reflects changes immediately (before server response) for a "desktop-like" feel.
6.  **Clean API**: All endpoints return standardized Pydantic models.

## AI Integration (Future Roadmap)

### AI Agent

A built-in AI assistant to help users:

- **Search**: Find documents and answers using natural language.
- **Automate**: Suggest task breakdowns and project structures.
- **Summarize**: Generate summaries of project progress and document content.
