# FocusLog

A local-first Linux desktop application for focus management, activity tracking, and personal time analysis.

> **Status:** Planning · **Version:** 0.1 · **Target:** Linux desktop (initially Ubuntu)

## Vision

FocusLog combines a compact floating focus widget with a full dashboard. It helps the user answer three questions:

1. What am I working on right now?
2. Where did my time go today?
3. What should I focus on next?

The project is intentionally incremental: build a small, reliable tool that is useful early, then extend it based on actual use.

## Core principles

- **Local-first:** the application works offline; the local database is authoritative.
- **Reliable tracking:** sessions survive application restarts and unexpected crashes.
- **Low distraction:** the interface should make starting and maintaining focus easier, not create more administration.
- **Human-readable data:** records can be exported to Markdown, CSV, and JSON.
- **Git-friendly, not Git-dependent:** Git provides history and portability; it is not the live database.
- **Incremental engineering:** each milestone should be independently testable.

## Planned experience

### Floating focus widget
- Local 24-hour clock
- Current project/task or activity
- Elapsed active time
- Start, pause, resume, and stop controls
- Clear idle/running/paused state

### Main dashboard
- Today timeline and session history
- Project and task management
- Daily and weekly summaries
- Time distribution by project/category
- Session notes and tags

## Initial technology direction

| Area | Candidate |
|---|---|
| Language | Python |
| Desktop UI | PySide6 |
| Local persistence | SQLite |
| Export | Markdown / CSV / JSON |
| Version control | Git |
| Remote backup/collaboration | GitHub |
| Tests | pytest |

These are initial choices, not irreversible commitments. A small technical spike will validate desktop integration on Ubuntu Wayland, especially floating-window behavior.

## MVP definition

The first usable milestone is deliberately narrow:

1. Show the current local time.
2. Select or enter an activity.
3. Start, pause, resume, and stop one session.
4. Persist session data in SQLite.
5. Recover sensibly after restarting the application.
6. List previously recorded sessions.

The dashboard, analytics, and GitHub synchronization are later milestones.

## Development cadence

This is a side project, with approximately **two hours per day when time permits** and no hard deadline. Prefer small sessions with a concrete outcome: one tested behavior, one documented decision, or one validated experiment.

## Documentation

- [Requirements](docs/REQUIREMENTS.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Roadmap](docs/ROADMAP.md)
- [Architecture decisions](docs/DECISIONS.md)

## Non-goals for the first version

- Always-on surveillance or automatic tracking of every application
- Cloud-first storage
- Complex team/project management
- AI features before the activity data model is stable
- Frequent Git commits for every timer tick

## License

Not selected yet.
