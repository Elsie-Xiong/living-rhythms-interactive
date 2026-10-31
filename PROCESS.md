# Process

## Starting Idea

The project began as an extension of my previous elephant movement visualisation.

The earlier version focused mainly on showing the collective daily movement rhythm of 14 tracked elephants and presenting movement data through a more analytical interface. For Assignment 3, I wanted to move beyond a static or dashboard-style visualisation and create a more immersive interactive experience where the user could explore the movement landscape directly.

My initial interaction idea was relatively simple:

- show the collective movement rhythm,
- allow the user to select one elephant,
- compare its hourly movement with the collective median,
- and allow the user to move through a 24-hour timeline.

This early version worked technically, but it still felt too close to a conventional data dashboard. The map, selector, timeline and comparison chart behaved as separate interface components rather than one connected experience.

---

## Early Functional Prototype

I first built a functional version around individual-versus-collective comparison.

The project added:

- an elephant selector,
- individual hourly median movement data,
- a 24-hour comparison between one elephant and the collective pattern,
- and an interactive time scrubber.

This version successfully created a clear input-response relationship. Selecting an elephant changed the highlighted trajectory and the comparison data, while changing the time updated the movement field and values.

However, after testing the interaction myself, I felt that the experience was still too fragmented. The user was mostly operating interface controls around the visualisation rather than exploring the visualisation itself.

This led to a major design change.

---

## Spatial Narrative Redesign

I redesigned the interaction as a spatial narrative experience.

Instead of treating the visualisation as a dashboard, the movement landscape became the main interface. The experience was organised around a full-day rhythm with five narrative phases:

1. Quiet Hours
2. Morning Rise
3. Midday Drift
4. Afternoon Peak
5. Night Return

The experience begins automatically at 02:00 and moves through the day. Movement segments, particles, visual intensity and narrative text change with time.

Users can also explore the landscape spatially by:

- scrolling to zoom,
- dragging to move,
- hovering over trajectories,
- and clicking an elephant trajectory to follow an individual.

The goal of this redesign was to shift the experience from:

**select → read → compare**

toward:

**explore → encounter → follow → discover**

---

## Performance and Visual Refinement

The first spatial version created a stronger sense of immersion, but the animation became less smooth when too many visual elements were drawn at once.

I therefore refined the rendering logic by limiting the number of movement segments drawn in each frame and adjusting particle density according to collective movement intensity.

I also adjusted brightness and transition values several times.

One intermediate version made the movement patterns more visible, but the brightness changes became too abrupt. I changed the visual energy system again so that movement intensity increased and decreased more gradually across the day.

This was especially important around the Morning Rise and Afternoon Peak sections, where the visual rhythm needed to feel stronger without appearing to jump suddenly.

---

## User Trial

I asked another person to try the experience before explaining how it worked.

The main observations were:

- The tester understood that they should click **ENTER THE HERD**.
- They understood the overall topic and movement-based theme.
- They did not immediately understand that a highlighted trajectory represented one individual elephant.
- They wanted clearer visual guidance about what could be clicked.
- They noticed the chapter changes, but felt that some transitions were not smooth enough and appeared to jump.
- They felt that the automatic time progression was slightly too fast.
- They wanted to click and enlarge individual trajectories.
- After zooming into an individual trajectory, they still found it difficult to understand where the elephant had moved geographically.
- They suggested adding environmental or geographic context such as a map, coordinates or terrain while keeping the visual style consistent.
- They generally liked the visual atmosphere and dynamic quality of the experience.

This trial directly informed several later changes.

---

The most important decision from this trial was not to add more decorative features, but to make the existing interaction easier to understand: clarify what an individual trajectory means, stabilise the spatial frame, provide geographic context, and give the user direct control over time.

## Changes Made After User Testing

### 1. Clearer trajectory interaction

I added clearer hover feedback so that moving over a trajectory reveals the elephant ID and explains that the line represents one elephant's historical movement footprint.

The hover message also explains that clicking the trajectory opens its individual rhythm.

This was added because the tester did not initially understand what the highlighted path represented.

---

### 2. Geographic context

I added:

- longitude and latitude grid lines,
- Kruger National Park location information,
- a north indicator,
- and a scale bar.

These elements provide spatial context without adding a visually dominant map layer.

I deliberately did not use a detailed terrain background because I wanted the movement trajectories to remain the main visual material.

---

### 3. Stable spatial frame

An earlier version automatically changed the camera position when the experience entered a new narrative chapter.

After seeing this in use, I found that it made the entire map appear to jump between chapters and made it difficult to build a stable spatial understanding.

I removed the automatic chapter camera movement.

The final principle became:

**space stays stable while time changes inside it.**

The camera now moves automatically only when the user deliberately selects an individual elephant.

---

### 4. Deeper individual exploration

The individual elephant view was expanded from a simple information card into an individual movement dossier.

It now includes:

- current individual median movement,
- collective herd median,
- difference from the herd,
- a 24-hour individual-versus-herd rhythm graph,
- peak movement hour,
- quietest movement hour,
- largest divergence from the herd,
- and an explanation of the difference between the historical movement footprint and the current hourly movement field.

This helped make the individual view more meaningful instead of only enlarging a trajectory.

---

### 5. Improved individual layout

The expanded dossier initially covered too much of the selected trajectory.

I changed the individual camera composition so that the selected elephant is positioned further to the left while the dossier remains on the right.

This creates a clearer two-part composition:

**left: movement trajectory**  
**right: movement information**

---

### 6. Manual time exploration

The experience originally progressed automatically through the day.

I later added a draggable timeline so the user can directly inspect different periods.

When the user drags the timeline:

- automatic playback pauses,
- the displayed time changes,
- the movement field updates,
- the chapter state updates,
- and the selected elephant's dossier and rhythm graph update.

If the experience was playing before the user dragged the timeline, automatic playback resumes shortly after they release it.

This keeps the narrative flow while also allowing deliberate exploration.

---

### 7. Interaction guidance

I added temporary interaction hints that appear and disappear automatically.

These explain actions such as:

- scrolling to zoom,
- dragging to explore the map,
- hovering over a trajectory,
- clicking an elephant,
- dragging the timeline,
- and using keyboard controls.

I chose temporary hints rather than permanent instructions because permanent interface labels would reduce the immersive visual quality of the experience.

---

## Data and Interaction Decisions

The project uses GPS tracking data collected between 2007 and 2009.

The visual experience presents a 24-hour rhythm, but this does **not** represent one continuous recorded day.

Movement observations are grouped by local hour across the full study period.

The statistical comparisons use hourly median movement based on valid approximately 30-minute movement steps.

The browser trajectory and movement layers are downsampled for performance, while the hourly statistical summaries use the full set of valid movement steps.

To avoid implying false precision, the interface explicitly states that:

**statistics remain hourly while visual transitions are interpolated.**

The individual view also labels the current hourly bin so the user can distinguish the animated visual transition from the underlying statistical resolution.

---

## AI Use

I used ChatGPT during the development process.

It was mainly used for:

- debugging HTML and JavaScript,
- discussing interaction structures,
- generating and revising code prototypes,
- improving animation performance,
- exploring alternative interface layouts,
- and helping organise documentation.

I did not accept every AI suggestion directly.

Each major change was tested in the browser and adjusted based on the actual visual and interaction result.

---

## One AI-Supported Suggestion I Kept

One useful suggestion was to move away from the early dashboard-style interface and develop the project as a spatial narrative experience.

This idea matched my goal of making the movement data feel more explorable and immersive.

I kept this direction and developed it further through:

- automatic narrative time progression,
- spatial trajectory exploration,
- narrative chapters,
- individual encounters,
- geographic context,
- and time-based movement changes.

The final implementation is substantially different from the earlier selector-and-chart prototype.

---

## One Suggestion I Changed or Rejected

Several ideas were changed or rejected during development.

One early direction involved using terrain elevation data as an additional visual layer.

I tested this direction but decided not to continue with it because it increased complexity without clearly improving the core interaction between the user and the movement rhythm.

Another design idea used automatic camera movement between narrative chapters.

Although this created a cinematic effect, I later rejected it because the geographic frame shifted whenever the chapter changed. This made the spatial relationship harder to understand.

I replaced it with a stable global map frame and kept automatic camera focus only for deliberate individual selection.

This became one of the most important interaction decisions in the final version.

---

## Development History

The Git history records the project as it developed rather than only showing the final version.

Major development stages include:

- starting Assignment 3 from the previous interactive baseline,
- adding individual hourly rhythm data,
- adding individual-versus-collective comparison,
- adding an interactive time scrubber,
- redesigning the interface as a narrative spatial experience,
- improving narrative animation performance,
- refining chapter transitions,
- adding geographic context,
- expanding individual exploration,
- and improving the final interaction layout.

I used commits at meaningful milestones so that the repository shows both technical development and design decisions rather than only the finished result.

---

## Final Interaction

The final experience combines automatic narrative progression with direct user control.

The main interaction loop is:

**explore the collective movement field → discover an individual → follow its trajectory → inspect its rhythm → change time → compare with the herd → return to the collective field**

The project therefore extends the earlier visualisation not simply by adding controls, but by changing the relationship between the user and the data from passive observation to spatial exploration.