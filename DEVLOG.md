# Devlog

## #011 · 17 Oct 2026 · Six new buildings

**Ask:** a Morning Dispatch, a Studio workshop, a Habit Garden, a world-news place, a Sunday review, a coursework tracker, and a Focus Lighthouse that sums up my focus every week.

**Morning Dispatch** (newsstand with a rising-sun sign, front of the HQ)
- **Brief:** at 07:22 UK time every day, a scheduled Claude run writes a 3–4 sentence brief. It covers what's due, deadlines this week, habits, any Barça or Spain match, a headline worth knowing, and one suggestion for the day. It shows on the island only, with no notifications.
- **Live summary:** the Today tab also builds a live summary from the island itself: due to-dos (tick them off right there), this week's deadlines, habit chips, this week's focus, upcoming matches and the top 3 headlines.
- **Week review tab:** the Sunday review lives here. It runs every Sunday at 18:46 and covers:
  - what got done and what slipped
  - focus time with a written summary
  - habits against their targets
  - the top 3 priorities for next week

  A button writes it on demand too.

**News Tower** (lattice broadcast mast on its own islet off the east edge, joined by a NEWS / ON AIR skyway)
- Sections: World (6), UK politics (up to 4), US politics (up to 4), Tech (5), Design (4).
- Each story gets a plain-English headline, one neutral sentence of context and a link to the source. It refreshes with the 07:22 run.
- **Sources:** this took some digging, because a lot of news sites block automated reading. The ones that work are Al Jazeera (world, UK, US), TechCrunch, Hacker News and Dezeen.

**Studio** (sawtooth-roof workshop with a jib crane, south-west park)
- **Projects:** next step, milestones with a progress bar, and links.
- **Post queue:** Instagram/GitHub posts move Ideas → Drafting → Ready → Posted. "Draft caption" asks Claude to write one in my voice: plain, no hype, hashtags for Instagram.
- **Seeded with** this project and the devlog #010/#011 posts.

**Habit Garden** (raised beds in the front park)
- **One bed per habit.** It starts with Gym (4× a week) and Sleep before midnight (daily).
- **Very slow growth:** every 8 check-ins bring one plant to full bloom, so a whole bed takes about 2 months. That fits the rule that progression has to be slow.
- **The panel has:**
  - a big "done today" button
  - a tappable week strip for backfilling
  - the streak and total
  - a 12-week heatmap

**Coursework observatory** (drum tower with a telescope and an orbit ring, front-right plot)
- **Deadlines:** each piece has a module, due date and weight. The tiles show the next deadline, the next 14 days and how much of the year's marks are still in play.
- **Urgency colours:** amber inside a week, red inside 3 days.
- **Quick actions:** start / submitted, "+ to-do", and "Focus" (opens the lighthouse with the piece already filled in).

**Focus Lighthouse** (striped lighthouse next to the Mail building)
- **Sessions:** 25, 50 or 90 minutes, tagged with an area or a module.
- **While it runs:** the lighthouse beam switches on across the island, a timer pill sits at the top of the screen, and the session survives a page reload.
- **Week view:** a Mon–Sun bar chart and a breakdown by area.
- **Weekly summary:** the Sunday review writes it, and "Summarise my week" writes one on demand.

**Fixes along the way**
- **Click areas:** a building's invisible click area could sit on top of the building next to it, so clicking the HQ opened the lighthouse. All click areas now live in one layer underneath every building, so the shape you see always wins.
- **Glow halos** no longer block clicks.

**Tests:** all 12 buildings open with a real click at desktop and narrow widths. 36 out of 36 clicks worked straight after scroll-pans, pinches and drags. No page errors.

**Media:** `media/v0.8-island.png`, `media/v0.8-panels.png`, `media/v0.8-lighthouse-on.png`

## #010 · 17 Oct 2026 · La Roja islet, Champions League, smarter refresh

**Ask:** a building for the Spain national team on the left islet, Champions League data for Barça, and less frequent refreshing, unless a game is live.

**La Roja islet (Spain)**
- The empty expansion islet on the left is now a square floating deck. It's joined to the island by its own skyway, which carries the west road over the gap and has red and gold rails and gantries reading ESP and LA ROJA.
- On the deck is a red and gold arena. I turned the Barça stadium into a reusable `arena()` function, so both grounds share one design with different colours.
- A pylon next to the arena carries a gold neon star. In the UEFA data, Spain won the 2026 World Cup, beating Argentina 1-0 after extra time.
- The arena's LED scoreboard shows the next match, e.g. `CZE v ESP · THU 12 NOV`.

**The Spain panel** (red and gold frame) uses the same Matches / Live / Stats layout as Barça. Under the hood it's one football module that serves both teams.
- **Matches:** upcoming and results, with competition filters (Nations League, World Cup, Friendly).
- **Live:** the scoreboard, plus a centred goal timeline in Sofascore style: home events on the left, away on the right.
- **Stats:**
  - World Cup badge
  - Nations League position, record, goals and form
  - Unbeaten run and facts
  - Top scorers this season and at the World Cup
  - Nations League group table with qualification zones

**Champions League in the Barça panel**
- **Match filter:** the match lists now have competition chips (All, LaLiga, UCL…).
- **Stats toggle:** Stats switches between LaLiga and Champions League. The UCL view shows:
  - League-phase position, record and goals, and the next opponent
  - Barça's UCL scorers and assists
  - Competition-wide top scorers and assisters
  - The full 36-team table, coloured by zone: round of 16, play-off, out
- **Source:** UEFA's own data feeds, which turned out to be the most reliable source so far.

**Refreshing: daily, plus live only during games**
- I replaced the hourly task with a daily refresh at 08:53 (UK time) that covers Barça, the Champions League and Spain.
- A second task, "Football live updates", only wakes up for a match: 25 minutes after kick-off, then every 25 minutes until full time. After that it books itself for the next Barça or Spain kick-off. The daily run double-checks that booking.
- On a quiet day that's 1 run instead of 12. On a match day it's about 6.

**Tests:** all 6 buildings open with a real click at desktop and narrow widths. 18 out of 18 clicks worked straight after scroll-pans, pinches and drags.

**Media:** `media/v0.7-la-roja-islet.png`, `media/v0.7-spain-stats.png`, `media/v0.7-barca-ucl.png`

## #009 · 17 Oct 2026 · Gesture polish: no flashing, no stuck clicks

Feedback on v0.6.2: zooming flashed, panning lit things up instead of moving cleanly, and clicks worked only some of the time.

**"Highlights things instead of panning."** During a trackpad scroll the cursor stays still while the map slides underneath it. The browser keeps sending hover events, so every building passing under the cursor lit up and popped its name tag.
- **Fix:** hover effects are off while the map is moving and for about half a second after. Dragging also clears any open tag, and text selection is disabled on the map, so a drag can't highlight the title or labels.

**"Clicks randomly stop working."** Two causes:
- **Lost releases.** If you pressed on the map and released somewhere else, the app never heard the release. It then thought a button was still held, so the next click counted as a drag. Now every press captures its release, and a mouse moving with no button pressed resets the state.
- **Tags covering buildings.** Hover tags were clickable, so a tag left over from the last building could sit on top of the next one and take the click. Tags are now labels only, and whatever building is under the cursor always wins. Clicking the tag itself still opens its building if there's nothing behind it.

**Flashing while zooming**
- The sky was a 9,000-unit SVG rectangle, which made one enormous layer, and zooming out exposed parts of it that weren't drawn yet. The sky is now a CSS gradient behind the island.
- The sharp redraw now waits 260 ms after the motion stops instead of 170 ms, so it happens less often mid-gesture.
- The time-of-day colours now reach all three layers. The front clouds were missing the day colours.

**Tests:** clicked all 5 buildings 3 times each, straight after a scroll-pan, a pinch and a drag, with 3 px of click wobble: 15/15 opened. Pressing, losing the release and then clicking Mail opens it. A scroll-pan over Task HQ shows no tags.

## #008 · 17 Oct 2026 · Input overhaul: click, pan, pinch, hover

**Bug: half the island ignored the mouse.** The real cause was one CSS rule. The building panel is a fixed-position `<aside>` that sits `hidden` when closed. My stylesheet gave it `display:flex`, which beats the browser's default `[hidden]{display:none}`. My test page added `[hidden]{display:none!important}`, so everything worked in testing. The live host page doesn't add that rule, so on the real site an invisible, empty 440 px panel sat over the right side of the map and swallowed every click, hover and scroll there. That's why the Stadium and Mail never opened. On a narrow window it covered the whole bottom half of the island.
- **Fix:** one line, `[hidden]{display:none!important}`, now ships inside the app itself.
- **Lesson:** test with the same page wrapper the real host uses, not a nicer one.

**Trackpad gestures now behave like a map app**
- Two-finger scroll pans in any direction. Before, it zoomed, so panning felt impossible.
- Pinch zooms. That's ctrl+wheel in Chrome and the Claude app, gesture events in Safari.
- Click and drag still pans, and arrow keys pan too. `+`, `-` and `0` zoom and fit.

**Performance:** before this, idle ran at 29 fps and every zoom frame redrew 2,500 SVG shapes (~100 ms).
- **Layers:** the scene is split into three stacked SVG layers. The back layer holds the sky, stars, moon and passing ships. The middle layer is the island, kept still so the GPU can cache it. The front layer holds the light waterfalls, drones and foreground clouds. Ambient motion only repaints its own thin layer.
- **Gestures:** while you pan or pinch, the already-drawn layers are just slid and scaled with one GPU transform. The real redraw happens once, about 170 ms after you stop.
- **Result** (same test machine, 2× retina): idle went from 29 to 60 fps, and pan frames from ~100 ms to ~20 ms.
- **Cars** on the ring road are now parked rather than driving. Their motion was forcing the whole island layer to repaint.

**Hover:** each building now has an invisible hit-pad under it, so the pointer doesn't fall through the gaps between its shapes and flicker the tag.

**Tests:** all five buildings open with a real mouse click at desktop and narrow widths. Also tested: hover, then click the tag; two-finger pan; pinch; drag; arrow keys.

## #007 · 17 Oct 2026 · Stadium islet + skyway, click fix

**Bug: buildings wouldn't open.** Hovering a building pops up its tag above it, but as soon as the pointer left the building to reach the tag, the tag hid itself. Clicking where the tag had been then hit empty floor. On the stadium the tag even flickered, because it popped up right under the cursor.
- **Fix:** hovering the tag now keeps it open. There's also a 650 ms grace period, so the pointer can travel from a building up to its tag. Taps are more forgiving too: up to 14 px of wobble, or 8 px if it's quick, still counts as a click rather than a drag.
- I tested it with simulated real mouse movement: hover the building, move to the tag, click. All five buildings open.

**Stadium moved to its own floating islet** behind the right edge of the island:
- **The islet:** rock underside with neon cracks, a deck with a gold neon border, and two glowing trees.
- **The skyway:** the south spoke road carries straight on over a cyberpunk skyway. It has a striped deck, neon rails, pulsing lane lights, two gantries with neon signs (FCB, STADIUM) and hanging under-lights.
- **The old spot:** the front park on the main island is back to trees and crystals.

**Media:** `media/v0.6.1-stadium-islet.png`, `media/v0.6.1-skyway.png`

## #006 · 17 Oct 2026 · Blaugrana Stadium (FC Barcelona)

**Ask:** a section for FC Barcelona, themed after the club, with the fixture list, past results, a scoreboard for live matches, and a Sofascore-style stats tab.

**In the scene:** a stadium on the front of the island.
- Blue and garnet striped walls with arched entrances and a gold neon rim.
- Stands in alternating rows, a sunken pitch with mowing stripes and markings, and four floodlight masts.
- An LED scoreboard over the back stand. It shows the live score while a match is on, otherwise the next fixture (e.g. `PSG v BAR · TUE 20:00`).
- A red LIVE pip appears on the stadium while Barça are playing.

**The panel** (blaugrana frame, gold neon title):
- **Matches:** Upcoming and Results, grouped by month. Each row has the date and time, competition and matchday, both teams, the score, and a W/D/L badge, laid out like Sofascore.
- **Live:** a scoreboard with the score, a LIVE badge, a goal timeline (scorer, minute, assist), and home/away comparison bars for match stats. When nothing is on, it shows the next match with a countdown and the last result.
- **Stats:**
  - LaLiga position, W-D-L, goals for and against, clean sheets
  - last-5 form, Champions League record and club facts
  - top players by rating (Sofascore-style colour badges), goals, assists, G+A, xG, big chances, dribbles, tackles, interceptions, clean sheets and yellow cards
  - the full LaLiga table, with the Champions League places and relegation zone marked

**Data pipeline:**
- The artifact can't call external APIs, so the data lives in the artifact's database as one document.
- I seeded it today from fcbarcelona.com (schedule, results, standings, previews) and FotMob (player leaderboards).
- A **scheduled Claude task** refreshes it every hour from 12:00 to 23:00 UK time. It refetches the same pages and writes the updated document back, and it's told never to invent a score or stat.
- Honest limitation: the "live" score is only as fresh as the last refresh (up to an hour), and only when a source publishes it. True minute-by-minute live data would need a sports data connector.

**Season so far (as seeded):** 8/8 in LaLiga (34 scored, 7 conceded), 2/2 in the Champions League, and 10/10 in all competitions. Betis v Barça kicked off as this was built.

**Media:** `media/v0.6-stadium.png`, `media/v0.6-barca-matches.png`, `media/v0.6-barca-stats.png`

## #005 · 16 Oct 2026 · Floating neon sky-island + in-world UI

**Feedback on v0.4:**
- The domes and onion tops read like mosques. That wasn't the vibe.
- The UI (title, Island/List switch, add bar) looked like generic AI-generated UI and didn't match the world.

**New references:**
- floating isometric islands with glowing waterfalls, rock spires with neon cracks, and light beams linking them to small islets
- a floating cyber block with drones
- an isometric neon city tile with particle trees and ships trailing light
- two street-level neon scenes, used for mood

**What changed in the scene**
- **It's a floating island now.** A square city deck sits on stepped rock strata with pink and cyan neon cracks, hanging above a sea of clouds.
- **Waterfalls of light** pour over the front edges with animated streaks. A glowing purple river flows from a pond across the park and spills over the edge as one of them.
- **Streets:** a ring road around the HQ with four spokes to the edges. It has neon curbs, crosswalks, dashed lane lines, street lamps, and four cars with neon trims circling the HQ. The cars are drawn under the buildings, so the HQ correctly hides the ones behind it.
- **Angular towers with spires** instead of domes:
  - **Task HQ:** a stepped tower with a glowing pink-to-violet core, side pipes and a beacon antenna.
  - **Chrono Spire:** a tapered obelisk with a clock collar and a neon-edged spire.
  - **Data Post:** a depot with a giant neon MAIL sign on rooftop scaffolding and a satellite dish.
- **Nature:** particle trees (canopies made of glowing dots), yellow crystal clusters, and jagged rock spires with neon cracks on the corners.
- **Room to grow:** 4 empty plots on the island, plus 2 expansion islets floating behind it, linked by light beams.
- **Sky:** drones bobbing around the buildings, ships with light trails crossing the sky, and puffy cloud banks that drift.

**What changed in the UI**
- **One committed night look** that matches the scene, instead of the light/dark system styling.
- **Title:** a neon-tube sign (one letter flickers like a failing tube) with an amber LED dot-matrix ticker for the date and time.
- **Island/List switch:** neon tube words on a chamfered plate. The active one is lit and the other is a dark, unlit tube.
- **Add bar:** a holo console with a gradient neon frame, chamfered corners, scanlines, a `›` terminal prompt, a pink key-style ADD button, and an LED readout showing where your item will go.
- **Building panels:** chamfered neon-framed screens that glow in each building's colour, with neon-tube titles and LED subtitles. Dates use the LED face too.

**Engineering notes**
- CSS `filter` runs before `clip-path`, so a glow on a chamfered shape needs two layers: an outer element carries the drop-shadow, and an inner element does the clipping.
- The waterfalls are vertical gradient ribbons with dashed streaks whose `stroke-dashoffset` is animated.
- The cars follow the ring road using `animateMotion` with `rotate="auto"`.

**Media:** `media/v0.5-skyisland-night.png`, `media/v0.5-taskhq-panel.png`, `media/v0.5-mobile-calendar.png`

## #004 · 16 Oct 2026 · Less blocky, more whimsical

**Feedback on v0.3:** it was too blocky and geometric. It needed to feel more whimsical.

**What changed**
- **Round silhouettes everywhere.** About 40% of the city towers are now round and tiered, with balcony rings and onion-dome, dome or antenna tops. The box towers get bay-window bumps, striped scalloped awnings, rooftop gardens and little water tanks.
- **Round windows.** Every window is now a dot, made with round-capped dashed paths, so the city reads softer and more playful.
- **Icon signs** replace word signs: stars, hearts, moons, cups, fish, noodle bowls, lightning bolts and music notes.
- **Main buildings redrawn round:**
  - **Task HQ:** a cylinder tower with "TASK HQ" in neon curving around the front (an SVG `textPath` on the front arc), a balcony ring, a teal dome and a round checklist badge.
  - **Chrono Spire:** a slim tower with a clock drum and an onion top with a star.
  - **Data Post:** round, with arched windows, a scalloped awning over the door, a dish, and a curvy mail chute with capsules zipping down to a drone pad.
- **Platform details:**
  - a ring of string lights around the HQ, round plazas and curvy lanes
  - a fountain and three food kiosks with striped domes
  - blossom trees mixed in with the greenery
  - onion-domed turrets on the corners
  - arched undercroft walls with neon outlines
  - a scalloped edge and a little blimp drifting past

**Engineering notes**
- New helpers: `arcD` (the front arc of any cylinder at any height, used for windows, neon trims and the curved text), `onion`, `roundSign`, `awning` and `stringLights` (a quadratic curve with three offset dashed bulb strands).
- Cylinder shading uses one cached horizontal gradient per colour, generated on demand.

**Media:** `media/v0.4-city-night.png`, `media/v0.4-city-day.png`, `media/v0.4-taskhq-night.png`

## #003 · 16 Oct 2026 · Neon city platform

**Feedback on v0.2:**
- The island needed to be much bigger, with space for more buildings.
- The post office was hanging off the edge.
- The name signs were too much.
- Some floating blue light rings didn't sit right in the scene's depth.

**Reference:** a cyberpunk isometric base: a square plaza with a neon grid floor, set inside a dense neon city. I used it for the mood and layout only. All the art is original.

**What changed**
- **The island is now a raised city platform.** It's a 26×26 tile grid with a purple border band, pine planters along the rim, and neon edge lines. It stands on pillars above street-level roads with moving traffic.
- **Lots of room to grow.** The four buildings sit well inside the edges, and five empty plots (dashed neon outlines with orange marker cones) are ready for future buildings.
- **A procedural city all around it.** Back towers rise up to around 20 storeys, with window rows, blade signs and billboards. A lower district sits in front of and below the platform, and air-cars cross the skyline.
- **New buildings:**
  - **Task HQ (to-dos):** a glass tower with a neon checklist sign.
  - **Chrono Spire (calendar):** a pink neon clock that shows the real time.
  - **Data Post (mail):** a satellite dish, a parcel chute and a delivery drone.
  - **Idea Beacon (ideas):** a hologram lightbulb with scanlines over a projector pad. It glows brighter the more ideas you have.
- **Quieter UI:** name tags only appear when you hover over a building (or tap it, or tab to it). The only thing always on screen is a small count of to-dos due now.
- **Depth-correct lighting:** I removed the floating rings. Every light now sits on a surface (walls, floors, signs) or at a lamp head.
- **Restyled panels** to match: techy display type, violet/cyan/pink accents and square checkboxes.

**Engineering notes**
- I dropped the SVG blur filter. Neon is now drawn as three stacked strokes, which is much cheaper with around 4.7k elements on screen.
- Windows are a single dashed path per wall face. SVG restarts the dash pattern at each subpath, so each row of windows lines up neatly.

**Next**
- [ ] Use it for a week
- [ ] Test Outlook access (Imperial + personal)
- [ ] Decide what goes on the first empty plot

**Media:** `media/v0.3-platform-night.png`, `media/v0.3-platform-day.png`, `media/v0.3-taskhq-night.png`

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
