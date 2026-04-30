# Cloud Architecture Overview

This monorepo contains a browser-based React frontend and an Express API running as a single local application stack. The API persists task data in an in-memory SQLite store, so data exists only for the life of the running backend process.

```mermaid
flowchart LR
    User[User in Browser]
    Frontend[React Frontend\npackages/frontend]
    Api[Express API\npackages/backend]
    Store[(In-Memory SQLite Store)]

    User --> Frontend
    Frontend -->|HTTP /api/tasks| Api
    Api --> Store
    Store --> Api
    Api --> Frontend
```

## Create TODO Sequence

```mermaid
sequenceDiagram
    actor User
    participant Frontend as React Frontend
    participant Api as Express API
    participant Store as In-Memory SQLite Store

    User->>Frontend: Enter task details and submit form
    Frontend->>Api: POST /api/tasks
    Note over Frontend,Api: JSON body includes title, description, and optional due_date
    Api->>Api: Validate required title
    Api->>Store: Insert task record
    Store-->>Api: Return created task id
    Api->>Store: Select created task
    Store-->>Api: Return created task
    Api-->>Frontend: 201 Created with task payload
    Frontend->>Api: GET /api/tasks
    Api->>Store: Query tasks
    Store-->>Api: Return task list
    Api-->>Frontend: 200 OK with tasks
    Frontend-->>User: Render updated TODO list
```

## Notes

- The frontend is a React application served from the `packages/frontend` workspace.
- The backend is an Express application in `packages/backend`.
- Task data is stored in-process using an in-memory SQLite database.
- Because the store is in-memory, task data is reset when the backend restarts.