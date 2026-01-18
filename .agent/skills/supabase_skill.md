---
name: Supabase & RLS Skill
description: Expert guidance on Database Schema, Row Level Security, and Storage policies.
---

# Supabase & RLS Skill

## Core Principles

1.  **Security in DB**: "The database is the API". Trust no client.
2.  **Least Privilege**: Default deny policies. Explicitly grant access.

## Schema Strategy

### Auth Integration

- **`public.profiles`**: Automatically synced with `auth.users` via Trigger.
- **Roles**: Enum type (`owner`, `admin`, `worker`, `viewer`) stored in `profiles`.

### RLS Policies Guide

- **SELECT**: `auth.uid() = user_id` OR `(SELECT role FROM profiles WHERE id = auth.uid()) = 'admin'`.
- **INSERT**: Check if user has permission to create.
- **UPDATE**: Ensure user owns the record or is Admin.

### Storage

- Buckets must have RLS enabled.
- Policy: "Allow Upload" -> `bucket_id = 'project-files' AND auth.role() = 'authenticated'`.

## Migrations

- Use Supabase CLI or SQL scripts in `supabase/migrations`.
- Do not make manual changes in production Dashboard.
