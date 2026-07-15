---
name: meeting-notes-summarizer
description: Summarize and organize meeting notes from a transcript, recording, or raw notes into a structured Markdown summary (meeting topic, attendees, discussion points, decisions, and action items). Use this skill whenever the user asks to "彙整會議紀錄", "整理meeting notes", "summarize this meeting", "整理逐字稿", pastes a meeting transcript, or uploads a meeting recording/transcript file and wants it turned into organized notes — even if they don't use the exact word "skill" or "summarize."
---

# Meeting Notes Summarizer

Turns a raw meeting transcript, recording, or rough notes into a clean, structured Markdown summary.

## When to use this

Trigger this skill whenever the user:
- Pastes or uploads a meeting transcript (text file, Otter/Zoom/Teams auto-transcript, etc.)
- Uploads an audio/video recording of a meeting and wants notes from it
- Asks to "整理/彙整會議紀錄", "summarize this meeting", "organize these meeting notes", or similar
- Gives you rough, unstructured meeting notes and wants them cleaned up

## Step 1: Get the raw content

- **Text transcript**: read it directly (already in context, or read the uploaded file).
- **Audio/video recording**: this skill does not itself transcribe audio. Check whether a transcription tool is available (e.g., a connected transcription MCP, or ask the user to provide a transcript/captions). If no transcription tool is available, tell the user you need a text transcript to proceed, and ask them to upload one or paste the text.
- **Rough/scattered notes**: use as-is; treat unclear items as gaps to flag rather than invent details.

## Step 2: Extract the structured content

Read through the full transcript/notes before writing anything, so cross-references (e.g., a decision made early but revisited later) are captured correctly. Pull out:

1. **Meeting Topic** — infer from context if not explicitly stated
2. **Attendees** — list names/roles as mentioned; if a speaker is unidentified (e.g. "Speaker 2"), keep that label rather than guessing a name
3. **Discussion Points** — organize by theme/agenda item, not strictly chronological if the conversation jumped around. Keep each point concise — summarize the substance of the discussion, not a blow-by-blow transcript
4. **Decisions** — anything the group explicitly agreed on or resolved
5. **Action Items** — tasks that came out of the meeting. Capture owner and due date whenever mentioned; if either is missing, write "未指定" (unspecified) rather than leaving it blank or guessing

## Step 3: Write the output

Always output in Markdown, using this structure:

```markdown
# [Meeting Topic]

**日期**: [if known, else omit this line]
**與會者**: [Name1, Name2, Name3...]

## 討論重點

### [Theme/Topic 1]
- Key point
- Key point

### [Theme/Topic 2]
- Key point

## 決議事項
- Decision 1
- Decision 2

## 待辦事項
| 事項 | 負責人 | 期限 |
|------|--------|------|
| Task description | Owner or 未指定 | Date or 未指定 |
```

Notes on formatting:
- Omit a section entirely if there's genuinely nothing for it (e.g., no explicit decisions were made) rather than writing "無" — a missing section is cleaner than an empty one.
- Keep discussion points as concise bullet points in Claude's own words — do not reproduce long verbatim stretches of the transcript (copyright + readability).
- Deliver the summary directly in the chat as a Markdown-formatted response. Only create a downloadable `.md` file if the user asks to save/download it, or if the transcript is very long (multi-hour meeting) and a file is more practical for them to keep.

## Step 4: Flag gaps, don't guess

If the transcript is ambiguous, cuts off, or has unclear audio artifacts (e.g., "[inaudible]"), note this briefly under the relevant section rather than fabricating content to fill the gap. Accuracy matters more than completeness here — meeting notes get acted on.
