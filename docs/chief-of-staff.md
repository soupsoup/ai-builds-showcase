# Chief of Staff

A daily-briefing and operations system that turns scattered notes, tasks, calendar, and email into the next useful action — the operational layer an actual chief of staff would maintain, automated.

## The problem

Running a team means tracking the same five things constantly: what's urgent today, what's overdue, what got promised in a meeting that nobody followed up on, and what the week actually looks like once the calendar and the task list are read together instead of separately. None of that lives in one place by default. This system makes it live in one place.

## How it's built

The system is an Obsidian vault — markdown files for daily notes, people, and projects — paired with a generation layer that reads across that vault plus task, calendar, and email data, and compiles it into a single `dashboard_data.json` payload: urgent items, open tasks, today's calendar, unread email signal, meeting notes, quick captures, weekly wins, and two narrative blocks — a week-in-review and a week-ahead summary written in prose, not bullet points.

`dashboard.html` is a static, dependency-free renderer: it reads `dashboard_data.json` and builds the UI client-side — urgent banner, today's radar (tasks that are high-priority, due today, or overdue), a project-grouped task grid, a meetings list pulled from Granola call notes, and the two narrative sections. Task completion state persists in `localStorage`, so checking something off doesn't require touching the underlying data file.

A `memory/` directory holds durable context — people, projects, terminology, glossary — read by Claude Code on every session via `CLAUDE.md`/`AGENTS.md`, so briefings reference the right people and the right shorthand without re-explaining the org chart every time. Daily briefings get written to disk as dated markdown files, building a running archive of what mattered on any given day.

## What the dashboard actually decides

The interesting part isn't displaying data — it's the judgment calls in how data gets surfaced. "Today's radar" isn't just today's calendar; it's a filtered, prioritized view: high-priority tasks plus anything due today or already overdue, regardless of which project it belongs to. The week-ahead narrative isn't a list of due dates — it's generated prose that names the highest-priority overdue items and frames the week's shape, the way a chief of staff would brief you verbally rather than email you a spreadsheet.

## What's real vs. synthetic in this demo

The renderer, the data schema, and the narrative-generation logic are unchanged from the system I run daily. The demo's `DATA` object is entirely fictional — a fake team, fake projects, fake meetings — generated to match the real schema so the actual rendering logic (including the narrative builders) runs exactly as it would on my real vault, just pointed at a story that isn't mine.
