---
name: Backend Engineering Skill
description: Expert guidance on FastAPI, Pydantic, and Clean Architecture.
---

# Backend Engineering Skill

## Core Principles

1.  **Type Safety**: 100% Pydantic coverage for Requests and Responses.
2.  **Dependency Injection**: Use `Depends()` for all shared logic (Auth, DB session).
3.  **Modular**: One router per business domain (Users, Projects, Files).

## Tech Stack Guide

### FastAPI

- **Entry**: `main.py`.
- **Routers**: stored in `app/routers/`.
- **Schemas**: stored in `app/schemas/` (Pydantic models).

### Supabase Integration

- Use `supabase-py` client.
- **Auth**: Validate JWT in `app/dependencies.py`. Extract `user_id` and `role`.
- **RLS**: Do NOT implement RLS in Python if possible. Let Postgres handle it. If complex logic is needed, enforce in Service layer.

### Pattern: Service Layer

- **Routes** (`routers/`) -> **Services** (`services/`) -> **DB/Storage**.
- Logic stays in **Services**, not Routes.

## Best Practices

- **Error Handling**: Custom `HTTPException` with clear detail.
- **Async**: Always use `async def`.
