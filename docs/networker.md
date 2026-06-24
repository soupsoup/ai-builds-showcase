# Networker

A tool for deciding who in your network — and who in your network's network — is worth reconnecting with right now.

## The problem

Most people's network sits in LinkedIn as an undifferentiated list. Nobody ranks it. You scroll, recognize a name, vaguely remember they're "in tech somewhere," and move on. Built during my own job search, Networker exists because the question I actually had wasn't "who do I know" — it was "out of everyone I know, who should I message this week, and why."

## How it scores contacts

Every contact gets categorized, then scored 0–100, then bucketed into a tier. The categorization runs off two inputs you set once in Settings: your **domain keywords** (what you do — used to detect peers and hiring managers) and your **target industries/companies** (where you want to land).

Category and base score:

| Category | Base | Trigger |
|---|---|---|
| Hiring Manager | 85 | Senior title + domain match |
| Recruiter | 75 | Title matches a recruiter pattern |
| Target Company | 65 | Works at a company on your target list |
| Senior Connector | 50 | Senior title + industry match |
| Domain Peer | 55 | Title/company matches your domain keywords |
| Industry Contact | 30 | Company/industry match only |
| Senior Other | 20 | Senior title, no other match |
| Weak Tie | 5 | None of the above |

On top of the base score, bonuses stack: +15 for a target-company match that wasn't already the primary category, +10 for domain match, +5 for industry match, +8 for a first-degree connection made in the last 30 days (recency signals an active relationship), +6 if it's been over a year (signals "overdue"), and up to +12 for second-degree contacts based on how many mutual connections you share with them.

Final score maps to a tier: **65+** is Tier 1 (reach out now), **30–64** is Tier 2 (worth a touch), under 30 is Tier 3 (low priority). Every contact also carries a pipeline stage — cold, reached out, replied, met, referred, interviewing — so the tool tracks where an actual conversation stands, not just who's theoretically worth talking to.

## Second-degree discovery

The harder, more useful question is the one LinkedIn doesn't answer well: who do *my* connections know that I don't? Networker surfaces second-degree contacts — people connected to your first-degree network but not to you — and explains the path: which of your contacts can make the introduction, and why that person is worth meeting (mutual connection count, target-company match, role relevance). This is the actual "network effect" most people pay lip service to and never operationalize.

## Architecture

Single-page application — vanilla HTML/CSS/JS, no framework, no build step. State lives in a Supabase Postgres backend (synced across devices) with a localStorage mirror as an offline fallback, so the app keeps working and queues writes if the network drops. Settings, contacts, second-degree contacts, and job-search targets are all persisted as JSON blobs keyed to a single app-state row, loaded once on boot.

The scoring engine (`categorize()` / `smartScore()` / `tier()`) is pure functions over plain contact objects — no server-side logic, no API calls per contact. That keeps re-scoring instant when you change your domain keywords or target list: the whole network re-ranks client-side in milliseconds.

## What's real vs. synthetic in this demo

The scoring algorithm, tier logic, pipeline stages, and second-degree discovery UI are the actual production code. The demo seeds in fictional contacts (no real names, companies, or relationship history) and runs with no live Supabase connection — it's the real engine, fed fake data, so you can see how it ranks a network without me handing over mine.
