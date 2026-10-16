# Devlog

## #001 · 16 Oct 2026 · From a reel to a working Town Hall

**Where it started:** I saw a reel of someone who turned their daily organisation into an island, with a building for each part of their life. I use Notes and Calendar right now, and I wanted something more fun that still makes my day easier rather than distracting me from it.

**Decisions made today**
- **Platform:** a private app on claude.ai, using my Claude account for both storage and AI. It needs no maintenance and costs nothing extra. If it outgrows that, the frontend can move to a standalone web app later.
- **Art:** an original chunky isometric style, drawn completely in code. It's mobile-strategy-game flavoured but has no copied assets.
- **Progression:** left out of v1. If it comes later, it has to be slow, over months, so it never turns into the main event.
- **Accounts to connect later:** Imperial Outlook, personal Outlook and Gmail.

**What shipped (v0.1)**
- An island with 4 buildings: Town Hall (to-dos), Clock Tower (calendar), Post Office (mail) and a Lightbulb hot-air balloon (ideas). There are also 2 empty plots for future buildings, and a pier.
- **Quick-add bar:** type something like "gym legs tomorrow 7am" and it's filed under Fitness for tomorrow at 07:00 straight away. Claude then tidies it up in the background.
- **Category chips** (Auto / Academic / Fitness / Daily / Misc / Idea) for when you want to choose yourself.
- **Town Hall list**, grouped Overdue → Today → Tomorrow → This week → Later → Anytime. You can filter by category, tap a task to edit it, and undo anything.
- **Ideas balloon:** the glow gets stronger the more ideas you have. "Next steps" asks Claude for 3 small actions.
- **Real-time sky:** dawn, day, dusk and night follow the actual time. Windows light up at night, and the clock tower shows the real time.
- **List view** for days when the island would just get in the way.

**Design notes**
- The building name plates say what each building *does* (To-dos, Calendar, Mail, Ideas), not what it's called. That keeps things clear without turning it into a plain to-do list.
- The red badge only counts items due today or overdue, so it doesn't nag about everything.
- The bunting on the Town Hall uses the four category colours, which ties the building to the list.

**Next**
- [ ] Use it daily for a week and note any friction
- [ ] Send reference artwork for the art pass
- [ ] Check whether Imperial's Microsoft 365 allows the Outlook connector

**Media:** `media/v0.1-island-day.png`, `media/v0.1-townhall-dark.png`
