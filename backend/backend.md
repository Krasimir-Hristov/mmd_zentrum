# Backend Architecture (The Brain)

## Technology Stack

- **Framework**: FastAPI (Python 3.10+)
- **Database**: PostgreSQL (via Supabase)
- **Authentication**: Supabase Auth + JWT Verification Middleware
- **Storage**: Supabase Storage (S3-compatible)

## Core Responsibilities & Architecture

### 1. Modular Routing

The API is structured around domain-specific routers to ensure maintainability:

- `/users`: User management and profile data.
- `/projects`: Project creation, updates, and settings.
- `/files`: File upload, retrieval, and linking.

### 2. Security & Auth

- **JWT Verification**: Custom middleware validates Supabase tokens on every protected request.
- **Row Level Security (RLS)**: We rely on PostgreSQL Policies to ensure users can only access data permitted by their role (Owner, Admin, Worker, Viewer).

### 3. Data Validation

- **Pydantic Models**: All requests and responses are strictly typed using Pydantic schemas to ensure a "Clean API".

### 4. Role-Based Access Control (RBAC) Implementation

The backend enforces the following hierarchy:

- **Owner**: Immutable access to their projects.
- **Admin**: Can manage system-wide resources.
- **Worker**: Can update task statuses and upload files if permitted.
- **Viewer**: Read-only access to specific resources.

## Best Practices

- **Design-First**: Define the Pydantic models before writing the endpoint logic.
- **Scalability**: The structure allows for easy addition of AI modules in the future.
