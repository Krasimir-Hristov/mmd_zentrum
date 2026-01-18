# Frontend Architecture (The Interface)

## Technology Stack

### Framework & Core

- **Framework**: Next.js 16+ (App Router)
- **Language**: TypeScript (Strict mode)

### State Management

- **Server State**: TanStack Query (v5)
  - Used for caching, synchronization, and optimistic updates.
- **Client State**: Zustand
  - Used for global client-side state like Auth session and UI settings.

### UI & Styling

- **Styling Engine**: Tailwind CSS
- **Component Library**: shadcn/ui (Base)
- **Theme**: Slate (Customizable)
- **Icons**: Lucide React
- **Printing**: `react-to-print` for direct document printing capabilities.

## Architecture & Patterns

### 1. Atomic Design

Components are organized to be small, reusable, and focused:

- **Atoms**: Buttons, Badges, Inputs (shadcn/ui primitives).
- **Molecules**: Form groups, Search bars.
- **Organisms**: Complex sections like the Project Board or File Vault.

### 2. Optimistic Updates

To enable a "desktop-like" experience, the UI should reflect actions (like moving a task or renaming a file) _immediately_ using TanStack Query's optimistic updates, reverting only if the server request fails.

### 3. Folder Structure

- `/app`: Next.js App Router pages.
- `/components`: Reusable UI components.
- `/lib`: Utility functions and validaters.
- `/hooks`: Custom React hooks (often wrapping TanStack Query).
