# Architecture

**Status:** Initial proposal · **Version:** 0.1

## 1. Design approach

Start with a small modular desktop application (a modular monolith), not a distributed system. Keep timing and persistence logic independent of the GUI so they can be tested without opening a window.

## 2. High-level structure

```text
+---------------------------+
|       Presentation        |
|  Floating Widget / UI     |
|  Dashboard                |
+-------------+-------------+
              |
+-------------v-------------+
|      Application Core     |
|  Session Service          |
|  Project / Task Service   |
|  Reporting Service        |
+-------------+-------------+
              |
+-------------v-------------+
|       Domain Model        |
|  Session State Machine    |
|  Duration Rules           |
|  Project / Task Entities  |
+-------------+-------------+
              |
+-------------v-------------+
|     Persistence Layer     |
|  SQLite Repositories      |
+-------------+-------------+
              |
+-------------v-------------+
|     Export / Integration  |
|  Markdown / CSV / JSON    |
|  Git (later)              |
+---------------------------+
```

## 3. Candidate source layout

```text
src/focuslog/
  app.py
  domain/
    models.py
    session.py
  services/
    session_service.py
  persistence/
    database.py
    repositories.py
  ui/
    widget.py
    dashboard.py
  export/
tests/
docs/
```

This is a target sketch. Create modules only when implementation needs them; avoid empty scaffolding.

## 4. Session timing model

The session service owns the state machine and duration accounting. The GUI sends commands; it does not calculate authoritative durations.

A robust implementation should record timestamped transitions (start, pause, resume, stop) or maintain equivalent accumulated active duration plus the current running interval.

For a running session:

`active_duration = accumulated_duration_before_current_run + (now - current_run_started_at)`

On pause, add the current run interval to accumulated duration and clear the running interval. On resume, set a new running start timestamp. On stop, finalize the current interval if running.

Use a monotonic clock for measuring intervals during a process lifetime where possible, and wall-clock timestamps for persistence and human-readable history. Recovery across process restart needs an explicit policy because monotonic clock values are not generally portable across boots.

## 5. Persistence

SQLite is the source of truth for live data. Store state transitions transactionally. Consider a schema migration mechanism before the database becomes difficult to change.

Git is for snapshots/exports and documentation history, not for writing each timer tick. A future export layer can generate deterministic daily files.

## 6. GUI and platform

PySide6 is the initial GUI candidate. Before committing to a floating-widget design, build a minimal experiment on Ubuntu GNOME/Wayland to validate:
- Window stays usable while other applications are focused.
- Always-on-top behavior is supported or has a practical fallback.
- Positioning and resizing behave acceptably.
- Closing/hiding the widget does not stop tracking.

If compositor limitations make a true always-on-top widget unreliable, use a small regular window or desktop panel/tray integration as the MVP fallback.

## 7. GitHub and AI integration

Initial direction:
1. Local SQLite database remains authoritative.
2. Export selected records to human-readable files.
3. Commit exports deliberately (for example, daily or on demand).
4. Sync to a private GitHub repository when configured.
5. Let external tools analyze exported records only when the user requests it.

Do not put secrets, tokens, or sensitive personal notes into the repository. Consider whether the repository should be private before adding real activity history.

## 8. Testing strategy

Prioritize domain tests before GUI tests:
- State transition validity
- Active duration across pause/resume
- Stop while running and while paused
- Restart/recovery policy
- Prevention of overlapping sessions
- Persistence and retrieval
