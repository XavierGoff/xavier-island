# Devlog

## #002 · 16 Oct 2026 · Steam by day, neon by night

**Feedback on v0.1:** it looked too childish, everything was crammed together, and it needed far more detail.

**Direction:** steampunk architecture that switches to neon after dark. It's driven by the real clock, so the island changes through the day: dawn, day, dusk, night.

**What changed**
- **Floating sky island.** The island is now a chunk of rock floating above a sea of clouds. The underside is layered strata with glowing crystals and hanging chains, and four brass levitation engines with spinning rotors hold it up.
- **Much bigger and more spread out.** The island is about 3× the area, with cobbled lanes and plazas between the buildings.
- **Pan and zoom.** Drag, scroll or pinch to move around. Tapping a building flies the camera to it, and a button recentres the view. The brass plaques are HTML, so they stay sharp at any zoom.
- **Every building redrawn with much more detail:**
  - **Guildhall (To-dos):** brick hall with stone columns, two rotating gear rose-windows, a verdigris mansard roof with porthole dormers, a brass drum and dome, steaming chimneys and pressure gauges. At night: a cyan "TO-DOS" neon sign with magenta trim.
  - **Clock Tower (Calendar):** an exposed gear train of four meshing gears, a 60-tick clock face showing the real time, and a spire with pinnacles. At night: neon rings around the clock faces.
  - **Pneumatic Post (Mail):** a riveted iron hall with a glass skylight and a copper sorting drum. Glass tubes run on posts to the Guildhall and the Clock Tower, with capsules moving through them. At night: a neon envelope sign.
  - **Lightbulb Airship (Ideas):** a glass bulb inside a brass cage, with a wooden gondola, propellers and fins, moored to a lattice mast. The filament glows at night, and the halo gets brighter as you add ideas.
- **New scenery:** a steam generator with copper boilers, a smokestack and a big ground gear; a water tower; a building site with a crane and scaffolding; gas lamps along the lanes; cypress trees; an iron railing around the edge; distant floating islets.
- **Night mode:** a colour-matrix filter darkens the island, and a separate glow layer adds lit windows, neon tubes, gas lamps, crystals and the capsules in the tubes.
- **UI restyle:** industrial signage type (Big Shoulders), engineering body and mono (IBM Plex), brass plaques and buttons, with cyan as the interactive accent in dark mode.

**Engineering notes**
- New primitives: `frustum` (mansard roofs), `cyl` and `dome` (shaded with metal gradients), `gearD` (procedural gear teeth with lightening holes), and `faceG(..., "T")` for drawing flat on the ground. That last one is how the big generator gear lies flat and spins.
- The camera stores `{cx, cy, w}` and derives the `viewBox` from the stage's aspect ratio, so resizing (for example when the side panel opens) keeps the view centred.

**Next**
- [ ] Use it for a week and note any friction
- [ ] Test Outlook access (Imperial + personal)
- [ ] Maybe: sound design (opt-in), more ambient life (birds, a small airship patrol)

**Media:** `media/v0.2-island-day.png`, `media/v0.2-island-night.png`, `media/v0.2-guildhall-night.png`

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
