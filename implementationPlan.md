# detailed Implementation Plan: MakroFlow (MMD_Zentrum)

This document outlines the step-by-step execution plan for building MakroFlow.

## Phase 1: Foundation & Setup

**Goal**: Initialize repositories and configure development environments.

1.  **Project Structure**
    - [x] Create root directory structure.
    - [x] Initialize Git repository.
    - [x] Create `.gitignore` (handling node_modules, venv, .env).

2.  **Backend Initialization (FastAPI)**
    - [x] Set up Python Environment (using `uv`).
    - [x] Install dependencies: `fastapi`, `uvicorn`, `supabase`, `pydantic`, `python-jose` (for JWT).
    - [x] Create entry point `main.py`.
    - [x] Configure Environment Variables (`.env`) for Supabase keys.

3.  **Frontend Initialization (Next.js 16+)**
    - [x] Run `npx create-next-app@latest` with TypeScript, Tailwind CSS, ESLint.
    - [x] Install Core Libraries: `lucide-react`, `clsx`, `tailwind-merge`.
    - [x] Install State Management: `@tanstack/react-query`, `zustand`.
    - [x] Initialize **shadcn/ui**: `npx shadcn-ui@latest init`.
    - [x] Add basic shadcn components: `button`, `input`, `card`, `dialog`.

## Phase 2: Database & Security (Supabase)

**Goal**: Design the schema and secure it with RLS.

1.  **Database Schema Design**
    - [ ] **Profiles Table**: Links to `auth.users`, stores roles (Owner, Admin, Worker, Viewer).
    - [ ] **Projects Table**: Title, Description, OwnerLink, Deadlines.
    - [ ] **Tasks Table**: ProjectLink, Status (Pending, InProgress, Complete), Assignee.
    - [ ] **Files Table**: Storage Path, Metadata, ProjectLinks (Many-to-Many if needed).

2.  **Role-Based Access Control (RLS)**
    - [ ] Enable Row Level Security on all tables.
    - [ ] Write Policies:
      - _Owner_: Full access to own projects.
      - _Admin_: Full access system-wide.
      - _Worker_: Update tasks, Read projects.
      - _Viewer_: Read-only.

3.  **Storage Buckets**
    - [ ] Create `project-files` bucket.
    - [ ] Configure storage policies for uploads/downloads based on Auth role.

## Phase 3: Backend Logic (FastAPI)

**Goal**: Create a strict, typed API with Authentication.

1.  **Authentication Middleware**
    - [ ] Create `verify_token` dependency to parse Supabase JWTs.
    - [ ] Inject `user_id` and `role` into request state for route handlers.

2.  **Routers Implementation**
    - [ ] **Users Router**: Endpoint to sync/get user profile.
    - [ ] **Projects Router**: CRUD for projects (enforcing RLS logic server-side).
    - [ ] **Tasks Router**: Endpoints for moving tasks (updating status).

3.  **Validation**
    - [ ] Define Pydantic models for _Request_ and _Response_ schemas.

## Phase 4: Frontend Core & UI

**Goal**: Build the responsive shell and design system.

1.  **Global App Layout**
    - [ ] Create `Sidebar` navigation (Links to Dashboard, Projects, Knowledge Base).
    - [ ] Implement `TopBar` with User Profile and Theme Toggle.

2.  **Authentication Integration**
    - [ ] Create Supabase Client Helper.
    - [ ] Build Login Page.
    - [ ] Create `AuthProvider` (Context) to protect private routes.
    - [ ] Store User Session in Zustand store.

3.  **Dashboard UI**
    - [ ] Create "Projects Overview" cards.
    - [ ] Display "My Tasks" summary.

## Phase 5: Functionality Implementation

1.  **Project Management**
    - [ ] **Create Project Modal**: Form with validation.
    - [ ] **Project Details Page**: Dynamic route `[projectId]`.
    - [ ] **Team Management**: Interface to add users to project (Admin/Owner only).

2.  **Task Board (Agile-Lite)**
    - [ ] Visualize tasks in columns (Pending, Progress, Complete).
    - [ ] Implement "Drag and Drop" or Simple "Move To" actions.
    - [ ] Apply **Optimistic Updates** with TanStack Query for instant UI feedback.

3.  **File Vault (Knowledge Base)**
    - [ ] **Upload Interface**: Drag & drop zone using Supabase Storage.
    - [ ] **File Viewer**: List/Grid view of PDF/Media.
    - [ ] **Link to Project**: Ability to attach a global file to a specific project scope.

4.  **Printing & Search**
    - [ ] Implement `react-to-print` for Project Summaries.
    - [ ] Create Global Search Bar (filtering local cache or query backend).

## Phase 6: Polish & Deployment

1.  **Optimization**
    - [ ] Lazy load heavy components.
    - [ ] Audit strict mode & types.
2.  **Final Review**
    - [ ] Test RBAC scenarios (Login as Worker, try to Admin actions).
    - [ ] Verify "Desktop-like" responsiveness.

## Phase 7: AI Agent Integration

**Goal**: Integrate an intelligent assistant to enhance productivity.

1.  **AI Backend Service**
    - [ ] Integrate OpenAI/Anthropic API or Local LLM.
    - [ ] Create endpoints for the AI Agent to query project data (RAG).

2.  **Frontend Chat Interface**
    - [ ] Add an AI Chat Widget or Sidebar.
    - [ ] Connect chat input to the backend AI service.

3.  **Capabilities**
    - [ ] **Natural Language Search**: "Find the contract for Project X."
    - [ ] **Task Automation**: "Create 5 tasks for the marketing phase."
    - [ ] **Summarization**: "Summarize the status of active projects."
