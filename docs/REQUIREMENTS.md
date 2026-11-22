# Requirements

**Status:** Draft · **Version:** 0.1

## 1. Purpose

Define the smallest useful behavior of FocusLog and the constraints that guide later implementation.

## 2. Primary use cases

- Start a focused work session against a project/task.
- Track an unstructured activity such as reading, exercise, a break, or administration.
- Pause a session without counting paused time as active work.
- Stop a session and retain its history.
- Review today's sessions and total time.
- Recover an in-progress session after an application restart.

## 3. Functional requirements

### FR-01 — Clock
Display the machine's local time in 24-hour format. The clock is informational and must remain distinct from the session timer.

### FR-02 — Session lifecycle
Support the states:
- **Idle:** no active session.
- **Running:** a session is accumulating active time.
- **Paused:** a session exists but is not accumulating active time.

Allowed transitions:
- Idle → Running: start
- Running → Paused: pause
- Paused → Running: resume
- Running/Paused → Idle: stop and save

Only one session may be active at a time.

### FR-03 — Session record
A session should retain, at minimum:
- Unique identifier
- Activity name
- Optional project and task identifiers
- Start timestamp
- End timestamp, when stopped
- Accumulated active duration
- Current/final state
- Optional notes and tags

Timestamps should be stored unambiguously (UTC internally, local time for display). Duration must not be inferred solely from a formatted clock string.

### FR-04 — Project and task basics
Allow the user to create, rename, and select projects and tasks. The first MVP may use a simple activity label and defer full project management.

### FR-05 — Persistence
Persist state changes promptly. A process crash or desktop restart must not silently discard already recorded time.

### FR-06 — Session recovery
On startup, detect a session that was running or paused when the application exited. Present a clear recovery choice or apply a documented recovery policy. Never silently invent an end time.

### FR-07 — History
Show saved sessions in chronological order, including activity, start/end, and active duration.

### FR-08 — Export
Later versions should export records to Markdown, CSV, and JSON without making exported files the primary database.

## 4. Reliability and edge cases

- Prevent overlapping active sessions.
- Define what happens when the user starts a new activity while another session is running.
- Handle pause/resume repeatedly without double-counting.
- Handle sleep, suspend, clock changes, and reboot.
- Avoid negative or implausible durations if the system clock changes.
- Make stopping an already stopped session safe (idempotent where practical).
- Do not lose a session if the UI closes unexpectedly.

## 5. Usability requirements

- Starting or pausing a session should take very few interactions.
- The widget should show the current activity and timer at a glance.
- The dashboard should not be required for routine start/pause/stop actions.
- Avoid gamification, excessive notifications, and distracting metrics.

## 6. Platform constraints

Initial target: Ubuntu Linux with GNOME/Wayland. Window positioning, always-on-top behavior, tray support, and autostart must be tested on the target desktop rather than assumed.

## 7. MVP acceptance criteria

The MVP is accepted when:
1. A user can start a named activity.
2. The timer advances while Running.
3. The timer does not advance while Paused.
4. Resume continues the same session.
5. Stop persists the final duration.
6. Closing and reopening the application preserves session history.
7. An interrupted session is detected and handled explicitly.
8. Automated tests cover lifecycle transitions and duration calculations.
