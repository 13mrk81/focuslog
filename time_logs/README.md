# Time Logs

This directory contains the manually reported activity history collected while FocusLog is being developed.

## File naming

Create one file per calendar day:

`YYYY-MM-DD.md`

Use the date stated by the user. Do not infer or silently convert time zones. Keep reported clock times as provided; if the timezone matters, record it in the daily heading or ask.

## Entry format

Each activity is recorded as one row:

| Start | End | Duration | Category | Activity | Notes |
|---|---|---:|---|---|---|

Rules:
- Use 24-hour time (`HH:MM`).
- Calculate duration from the stated start and end times.
- Do not invent missing start/end times. Mark unknown values as `—` and ask only when needed.
- Categories should stay consistent. Initial suggestions: `FPGA`, `FocusLog`, `Study`, `Work`, `University`, `Personal`, `Break`, `Sleep`, `Other`.
- Keep activity descriptions concise and factual.
- Preserve overlaps as reported; flag them rather than silently changing times.
- At the end of each day, include total tracked time and a short summary. Do not treat unreported time as a break or inactivity.

## Daily summary

Each daily file ends with:
- Total tracked duration
- Category totals (only where calculable)
- Unclassified / missing intervals, if any
- A brief factual note, without judgment

These are manual records, not an automatic tracker. Corrections should update the relevant daily file and be reflected in Git history.
