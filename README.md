# Stanford Frontier AI — Agents

Private study site. Built from official Stanford lectures, autumn 2026.

## What this is

Textbook-style courses that teach from zero: no prior machine
learning needed. Each lesson builds one idea at a time, with
worked examples, figures, interview Q&A, videos, and go-deeper links.

## What each course contains

- **Lessons.** Every lecture rebuilt as subchapters: one idea per
  subchapter, numbers and mechanisms throughout, no fluff.
- **Interview Q&A.** 6-8 per lesson with full follow-up answers.
- **Cheatsheet.** One dense page per course. Definitions, formulas,
  numbers, decisions, common mistakes.
- **Crash course.** One fast page per course. The whole story in
  30 minutes, with links into the deep lessons.

## Courses in this repo

- **CS329Z:** AI Agents
- **CS329A:** Advanced AI Agents
- **MS&E435:** AI Policy and Strategy

## Build

Content lives in `content/v2/` as Markdown. To rebuild:

```
python3 build/build.py content/v2 site/v2 "Stanford Frontier AI"
```

## Sources

Every lesson cites the official lecture video with timestamps, the
slides or lecture code, and the transcript. Nothing is invented.
Uncertain points carry an `[uncertain]` label. Model facts are
current as of October 2026.
