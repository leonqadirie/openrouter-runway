# OpenRouter Runway for TRMNL

**Know your balance. Keep shipping.**

A TRMNL plugin that displays your OpenRouter credit balance — so you never hit $0 mid-flow.

## The Problem

You're deep in a coding session, leaning on AI to move fast. Then your requests start failing. You've run out of credits.

Checking the OpenRouter dashboard means:
- Opening a browser tab
- Breaking your flow
- Context switching away from the problem you're solving

## The Solution

OpenRouter Runway puts your balance on your desk.

One glance tells you:
- **Current balance** — How much you have left
- **Credits spent** — To understand your cost-to-date

No surprises. No failed requests. Just a quiet reminder to refill before it matters.

## Features

- **Spend tracking** — See your usage trend at a glance
- **Live balance** — Syncs with your OpenRouter account
- **Poop emoji** — Once you have actually let your credits run out

## Future Plans

- **Per-model breakdown** — See which models are eating your credits
- **Budget alerts** — Custom thresholds for warnings
- **Spend rate** — How fast you're burning through credits

## Setup and Configuration

Create a new Private Plugin

Set strategy:

- Polling 
  - URL: https://openrouter.ai/api/v1/credits
  - Verb: GET

Add the website & API key within your TRMNL plugin setup


## Built With

- [TRMNL](https://usetrmnl.com) — The ambient display platform
- [Zed](https://zed.dev) — The editor we used to build this, fast enough to keep up with hackathon pace

---

*Built during the TRMNL Hackathon — because running out of credits shouldn't be a surprise.*
