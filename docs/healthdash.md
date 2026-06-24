# HealthDash

A health dashboard that gives feedback on your data instead of just plotting it — built around the lowest-friction capture method available: texting.

## The problem

Most fitness trackers ask you to open an app and log things in a form. That's the reason most logging dies after week two. The fastest way to actually capture what you ate or how you trained is to just say it, the way you'd tell a friend. HealthDash is built around that — capture has to be nearly free, or it stops happening.

## How it works

Food and exercise get logged by text message to Poke, which parses the message and writes structured entries into Notion — meals with estimated calories and macros, workouts with type, duration, and notes. Notion functions as the database: no separate logging UI to maintain, and the underlying data stays inspectable and editable in a tool that already exists.

HealthDash pulls from Notion and renders a dashboard: daily calorie and protein trends, a weekly workout chart, and a running log of entries in chronological order. The part that matters more than the chart is the commentary layer — instead of just showing "protein: 94g, target 130g," it's framed as a coach would frame it: pointing out a trend (three days under target), not just a single data point, and suggesting a specific, actionable fix for the next day rather than a generic reminder to "eat more protein."

## What it proves

A dashboard that only visualizes data answers "what happened." One that interprets data answers "what should I do about it" — the difference between a chart and a coach. That's the part AI is actually suited for here: not the capture (texting handles that), not the storage (Notion handles that), but noticing patterns across days and turning them into one specific instruction.

## What's real vs. synthetic in this demo

The dashboard layout, chart rendering, and coaching-commentary framing mirror the real tool. The demo's calorie counts, workout log, and coaching note are generated examples — not Anthony's actual logs.
