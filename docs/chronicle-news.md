# Chronicle News

A modern take on Circa — the mobile news app that broke stories into discrete, structured "atoms" readers could follow over time instead of re-reading a full article on every update. Two sides of one product: the editorial CMS where atoms get written, and the reader app where they get followed.

## The problem

Most breaking-news coverage forces a choice between a live blog (unstructured, hard to skim, no sense of what's actually new) and a fully rewritten article (structured, but buries the update in paragraph six). Atomic storytelling — discrete, timestamped facts attached to a persistent story — solves both: readers see exactly what's new since they last checked, and editors add information without rewriting a lede five times a day.

## The data model

A **Story** is the persistent container: title, summary, category, status (draft/published/archived). An **Atom** is a single fact or update attached to a story: type (text, image, video, or quote), rich content matched to that type, a position for ordering, source attribution, and an optional link to a related atom in a different story — so a development that affects two ongoing stories gets cross-referenced instead of duplicated. Atoms can be marked read individually, which is what drives the reader app's core mechanic.

## Editorial CMS (chronicle-web)

Next.js app, Supabase for auth and data (Postgres + row-level security), Tiptap for rich-text atom authoring, dnd-kit for drag-to-reorder atom sequencing within a story, and the Anthropic API wired in for editorial assistance — summarization and atom drafting from source material. An editor builds a story by adding atoms one at a time; each atom publishes independently, so a story can go live with one fact and grow over the next six hours without ever being "republished" as a whole.

## Reader app (chronicle-reader)

A from-scratch Next.js port of the original chronicle-ios SwiftUI app, replicating its actual business logic rather than just its look:

- **Following** shows only stories with unread atoms — a story you've fully read drops out of the tab automatically, the same way an inbox empties when you've read everything in it.
- **Wire** is a cross-story feed of every unread atom across everything you follow, newest first — built for someone tracking five stories at once who wants one feed, not five.
- Opening a story marks its atoms read and removes it from Following — viewing *is* the read receipt, no separate "mark as read" action required.

## What's real vs. synthetic in this demo

The atom/story data model, the CMS's editing and publishing flow, and the reader app's unread-tracking logic (Following dropout, Wire aggregation, follow/unfollow) are the real code, unchanged. Both demos run on fictional stories with stock imagery — no real sourcing, no real bylines.
