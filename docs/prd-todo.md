# Product Requirements Document (PRD) - TODO App Upgrade

## 1. Overview

Upgrade the basic TODO app so users can organize tasks with optional due dates, priority levels, and simple date-based filters while keeping the implementation lean and teachable. The MVP must remain local-only, with no backend changes or external storage.

---

## 2. MVP Scope

- Add an optional `dueDate` field stored as ISO `YYYY-MM-DD`.
- Add a `priority` field with allowed values `P1 | P2 | P3`.
- Default `priority` to `P3`.
- Add filter views for `All`, `Today`, and `Overdue`.
- Keep storage local only.
- Do not make backend changes.
- Validate task data as follows:
- `title` is required.
- `priority` must be `P1`, `P2`, or `P3`.
- `dueDate` is optional.
- Invalid `dueDate` values should be ignored and treated as absent.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks.
- Sort tasks in this order: overdue first, then priority (`P1` to `P3`), then due date ascending, with undated tasks last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user support.
- Keyboard navigation.
- External storage.