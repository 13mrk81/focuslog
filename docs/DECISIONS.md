# Architecture Decision Log

Record decisions that affect the structure or long-term behavior of FocusLog. Keep entries short; revisit them when evidence changes.

## D-001 — Local-first application

**Status:** Accepted

SQLite on the user's machine is the authoritative store. The application must work offline. Remote synchronization is secondary.

**Reason:** time tracking should remain available and reliable regardless of network access.

## D-002 — Git is for history and export, not live timing

**Status:** Accepted

Do not commit every timer tick or use Git as the live database.

**Reason:** frequent commits create noise and do not provide transactional application storage.

## D-003 — Modular monolith for the first versions

**Status:** Accepted

Keep UI, application services, domain logic, and persistence separated within one application.

**Reason:** this is a small personal desktop application; distributed components would add unnecessary complexity.

## D-004 — PySide6 is the initial GUI candidate

**Status:** Proposed

Validate it with a small Wayland desktop experiment before treating it as final.

**Reason:** Python enables rapid iteration, while Qt provides mature desktop UI capabilities. Wayland window-management behavior remains a platform validation item.

## D-005 — One active session at a time

**Status:** Accepted

The domain layer must prevent overlapping running sessions.

**Open detail:** decide whether starting a new activity automatically stops the previous session or asks the user first. Prefer an explicit, predictable interaction.
