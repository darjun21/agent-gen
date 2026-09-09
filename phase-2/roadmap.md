# Phase 2 Roadmap (Planned — Not Yet Built)

## Problem Phase 2 Solves

Phase 1's knowledge base is a static document, so Agent GEN correctly
declines to give exact live session times or current deadlines — it has no
way to verify them. Phase 2 aims to give the agent access to genuinely
current cohort data instead of a static snapshot.

## Proposed Architecture

Google Sheet (structured cohort events) → n8n → Current schedule/deadline
layer → Agent GEN

Google Sheet → n8n → Discord reminder / Opt-in SMS reminder

This would let Agent GEN support two directions:
- **Pull:** student asks "when is tomorrow's session?" and gets a current answer
- **Push:** Agent GEN proactively reminds students ahead of a session or deadline

## Proposed Google Sheet Schema (draft, not finalized)

| Field | Purpose |
|---|---|
| event_id | unique identifier |
| event_type | LIVE_SESSION / GUEST_LECTURE / PROJECT_DEADLINE / CERTIFICATION_DEADLINE / ANNOUNCEMENT |
| title | short name |
| description | detail |
| date | event date |
| start_time / end_time | timing |
| timezone | e.g. ET |
| deadline | for deadline-type events |
| submission_url / session_url | relevant link |
| status | active/cancelled/rescheduled |
| reminder_24h / reminder_1h | whether reminders are due |
| last_verified_at / verified_by | data freshness tracking |

## Planned n8n Workflows

1. Read current events from the Google Sheet
2. Serve current