# Roadmap

**Status:** Draft · **Cadence:** approximately 2 hours/day when available

The roadmap is outcome-based, not deadline-based. Each phase should end with a working demonstration.

## Phase 0 — Foundation
- [ ] Confirm repository visibility and project scope
- [ ] Add requirements and architecture documents
- [ ] Establish Python environment and test runner
- [ ] Record initial architecture decisions

**Exit condition:** project can be installed for development and tests can run.

## Phase 1 — Timing core
- [ ] Define session data model
- [ ] Implement Idle / Running / Paused state machine
- [ ] Implement active-duration accounting
- [ ] Add SQLite persistence
- [ ] Add unit tests for transitions and timing

**Exit condition:** session lifecycle works in a command-line test without a GUI.

## Phase 2 — Minimal desktop widget
- [ ] Validate PySide6 on Ubuntu Wayland
- [ ] Display 24-hour clock and active timer
- [ ] Add activity label and lifecycle controls
- [ ] Test hide/close/reopen behavior

**Exit condition:** a session can be tracked from the compact widget.

## Phase 3 — Recovery and history
- [ ] Define interrupted-session recovery policy
- [ ] Restore session state on application startup
- [ ] Show today's session history
- [ ] Test suspend/reboot and clock-change scenarios

**Exit condition:** records remain trustworthy after interruptions.

## Phase 4 — Projects and dashboard
- [ ] Add projects and tasks
- [ ] Add dashboard and daily timeline
- [ ] Add session notes and tags
- [ ] Add basic filtering

**Exit condition:** activities can be organized and reviewed.

## Phase 5 — Reports and export
- [ ] Daily and weekly summaries
- [ ] Project/category time totals
- [ ] Markdown / CSV / JSON export

**Exit condition:** data is useful outside the application.

## Phase 6 — Git integration
- [ ] Define export directory and file naming
- [ ] Add manual or scheduled Git commit workflow
- [ ] Add GitHub sync
- [ ] Document backup and conflict behavior

**Exit condition:** exported logs can be versioned without risking the local database.

## Phase 7 — AI-assisted analysis (optional)
- [ ] Define a privacy-conscious export format
- [ ] Generate summaries from selected logs
- [ ] Support planning based on historical effort
- [ ] Keep all AI actions user-initiated

**Exit condition:** AI analysis adds value without requiring live desktop access.

## Working rule

For a two-hour development session, choose one small deliverable. End by running tests, recording the result, and writing the next concrete step. Avoid expanding scope mid-session.
