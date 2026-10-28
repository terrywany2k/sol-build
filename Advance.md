# Solar System Agent Build - Advance

Copyright (c) 2026 Terry Wan. All rights reserved.

This notice applies to this brief. Submitted applications do not need to carry
Terry Wan's copyright notice; their authors retain ownership of their original
work, subject to applicable third-party rights and licenses.

## 1. Objective and starting material

Build an original browser observatory that combines a physically scaled Solar
System, a varied astronomical catalog, and practical Earth-based observing tools.
Choose and justify your own scientific models and implementation. This brief
does not prescribe methods, algorithms, frameworks, engines, or services.

Only this brief is provided. Independently acquire lawful scientific data and
visual assets, retain provenance, and comply with source and license terms.
This is a standalone edition with reduced catalog, companion-tool, and acceptance
requirements relative to Challenge.md. Basic.md's prescribed method does not
apply. All requirements below are mandatory except section 7's optional features.

The [reference observatory](https://starward-observatory.pages.dev/) may be
explored through its visible interface and ordinary browser interactions.
Normal browser loading and rendering are allowed. Do not inspect, extract,
download for analysis, or reuse its source, bundles, network-response bodies,
data, or visual assets, including copies from repositories, mirrors, caches,
archives, or third parties. Screenshots may document behavior but must not
become copied interface or texture assets. Use an original identity without
implying endorsement or ownership of the reference's work.

## 2. Catalog and physical scene

Provide at least the following independently sourced catalog:

| Category | Minimum breadth |
| --- | --- |
| Natural bodies | Sun, eight major planets, five dwarf planets, 20 moons, and six comets |
| Moon systems | Earth, Mars, Jupiter, Saturn, Uranus, and Neptune represented |
| Spacecraft | Six missions spanning at least three destinations |
| Artificial Earth satellites | Six entries representing low, medium, geostationary, and highly elliptical orbits |
| Sky | 3,000 catalog stars, 20 constellations with sourced connections, and 25 identified deep-sky targets |

Missing values remain unavailable. Distinguish physical centers from system
barycenters, and measured properties from illustrative or approximate models.

Use one documented physical length scale for positions, body radii, moon
separations, ring dimensions, and spacecraft. Do not individually enlarge
meshes or compress ordinary scene distances. Screen markers may remain readable
at fixed pixel size if separate from physical geometry. Unknown dimensions do
not become invented measured sizes.

Provide selection, search, focus/follow, parent-centered orbit framing, rotate,
pan, zoom, reset, labels, orbit layers, and sourced information panels. Include
rings where applicable and a size-comparison view for the planets and at least
ten moons; disclose any rearranged comparison spacing.

## 3. Time and trajectories

Accept scene and observation dates throughout 2000-2050. Individual models may
have narrower coverage, but must state and visibly enforce it, with no fabricated
positions or silent extrapolation. Pause, reverse, speed selection, precise
date entry, and UTC/local-time presentation must preserve the represented instant.
Document internal time scales, coordinate frames, units, and conversions.

Natural bodies and artificial objects must move along sourced, time-evaluated
trajectories with declared validity and quality. Orbit displays must explain
whether they represent a reference curve or a time-dependent track. Information
panels show sourced descriptions, dimensions when known, orbital information,
current coordinates, source links, and availability.

Provide an interactive trajectory view for at least one comet and one spacecraft,
with rotate/zoom/reset, time markers, and Sun/Earth distances. Hold or stop at
coverage boundaries. Leaving restores the prior scene and clock; interrupted
loading must not publish an obsolete view.

## 4. Earth observation and tonight planning

Provide an Earth observer with city selection or manual coordinates, a named
time zone, local altitude/azimuth, equatorial readouts, angular zoom, tracking,
and a geometric horizon. Explain the observer's reference surface and height.
Distinguish simultaneous exterior positions from received observer directions,
and account for applicable finite-distance parallax and light travel time.
State whether refraction, terrain, and atmospheric effects are included.

Show catalog stars, constellation connections, and selectable deep-sky targets
with source-qualified information. Treat catalog photometry and missing values
honestly; an illustrative image is not a measured surface or aligned sky map
unless its registration is established.

For a selected target and local civil date, provide an altitude curve and usable
observing windows from local noon to the next local noon. Include target-altitude,
darkness, and Moon-separation constraints with visible settings. Sampling must
be no coarser than ten minutes on ordinary nights; disclose exceptions and avoid
claiming exact event clocks or detectability from sampled windows.

Handle DST 23/25-hour nights, ambiguous times, skipped dates, and unavailable
source intervals explicitly. Export a useful observing table retaining the date,
site, time zone, constraints, and data coverage. Location storage and deletion
must be clear, without undisclosed transmission.

## 5. Scientific acceptance

Publish a readable explanation and machine-readable result table tied to the
exact application candidate. Comparisons identify source/version, target and
center, units, frame, time scale, epochs, and qualified coverage. Use independent
epochs not used for fitting, including interval endpoints and interior dates.

| Check | Required evidence |
| --- | --- |
| Planets and Moon | All eight planets and Earth's Moon, each at 20 independent epochs spanning a qualified interval of at least one year |
| Position agreement | Planets: maximum Cartesian residual <= 10,000 km and <= 0.1% of reference distance; Moon relative to Earth: <= 1,000 km and <= 1% |
| Other natural bodies | At least three additional moons across two systems and three comets, each at ten independent source-covered epochs; declare error targets before validation and report whether met |
| Artificial objects | At least three spacecraft and three satellites, each at ten source-covered epochs; report finite validity, model class, and measured errors against declared targets |
| Physical scale | Numerical dimension and distance checks for each rendered category, including a spacecraft relative to a planet without individual mesh enlargement |
| Observer direction | At least five independent site/time/target cases, including a near-horizon Moon and a daylight/night boundary; maximum angular direction difference <= 0.25 degrees under matched definitions |
| Planning | Numerical checks of altitude/darkness/Moon constraints, local-noon boundaries, and exported observing context |

For each position cohort report maximum absolute error, RMS, and percentage
error, including the epoch and reference distance at each maximum. Define
percentage as `100 * norm(model-reference) / norm(reference)` in the stated
center-relative frame and handle zero denominators explicitly. Report all
failures. Agreement for a qualified cohort does not qualify every catalog entry
or establish continuous accuracy throughout 2000-2050.

Additional catalog entries may use visibly qualified approximations with
documented evidence and coverage. Unsupported events or intervals remain
unavailable. Never invent source values, shift reference clocks, or present
predictions and artistic reconstructions as observations.

## 6. Operational acceptance and delivery

Deliver complete source, locked dependencies, reproducible source/asset
provenance and licenses, build/serve instructions, validation results, and a
working static distribution with a downloadable `dist.zip`. Support a documented
static-host subpath. Keep secrets and private records outside the distribution.

Report observed checks on at least one current desktop browser and one named
real mobile browser/device. Disclose the actual tested versions and environments;
emulation is supplementary and cannot establish real-device support.

- Build, cold load, reload, and warm-cache startup reach a usable scene; record
  readiness time and transfer size under stated device/network conditions.
- Missing data, a real 404, corrupt input, and retry show useful states without
  invented data or stale updates. Optional asset failure has a graceful fallback.
- At least ten open/close/switch cycles, including rapid cancellation, leave no
  accumulating owned contexts, listeners, or timers.
- Pause/reverse, coverage boundaries, DST nights, month/year rollover, invalid
  date entry, and return from trajectory views behave as declared.
- Keyboard selection, focus return, touch rotate/pinch, readable panels, and
  mobile scrolling remain usable. Demonstrate stable mobile interaction and
  report memory/resource observations and limitations.

Core requirements are scored out of 100 points: scientific correctness and honest limits 30;
catalog and feature completeness 25; interaction and mobile usability 20;
operational reliability 15; reproducibility and provenance 10. Prohibited copying,
fabricated scientific evidence, undisclosed source/license violations, or a
broken primary mobile experience prevent a passing submission.

## 7. Optional extensions

Larger catalogs, unbound comets, Galactic navigation, a surface landmark atlas,
surface observers on other worlds, full Journey telemetry, eclipse search/replay,
transit and moon-event theatres, a rolling 31-night calendar, multi-target
scheduling, star hopping, equipment/logbook tools, natal charts, offline support,
and signed release verification are optional for this edition. They cannot
replace the required physical scale, observing tools, or acceptance evidence.

## Overall assessment: 150 points

The maximum is 150 points: core requirements 100, additional UI/UX quality 30,
and additional features up to 20. Report all three subtotals separately. All
mandatory acceptance gates still apply regardless of the total score.

### UI/UX quality: 30 additional points

UI/UX is a major scoring category. Correct numbers alone do not make a usable
application. Evaluate the implemented experience on the edition's declared
desktop and mobile targets, using observed interaction rather than screenshots
alone. The core score covers required functional behavior; this additional
score assesses the quality of its presentation and use. Do not award points
twice for the same evidence of basic feature existence.

| Area | Points | What earns credit |
| --- | --- | --- |
| Visual hierarchy and readability | 6 | Legible text, contrast, clear units, coherent typography and spacing, and panels that preserve useful scene visibility |
| Discoverability and navigation | 6 | Understandable controls, clear selection and mode state, short paths to common tasks, and reliable back/reset behavior |
| Camera and direct manipulation | 6 | Predictable focus, follow, pan, zoom, and selection; controlled transitions without disorientation or accidental jumps |
| Responsive access and input | 6 | Practical touch targets, unclipped content, usable panel scrolling, keyboard access, visible focus, and layouts suited to the tested screens |
| Feedback and interaction flow | 6 | Responsive controls, clear time/loading/empty/error states, recoverable mistakes, and no stale or obstructive UI |
| Total additional UI/UX score | 30 | |

Demonstrate a first-use walkthrough: locate and select a body, inspect it, change
and pause time, adjust the camera, open and close information, and return to an
overview. For editions with observing tools, also set a site/date and inspect an
observing result. Include mobile touch and keyboard paths within the edition's
required device scope. Record friction and failures, not just the successful path.

A broken primary experience is a hard failure regardless of numerical accuracy
or total points: users must be able to complete these core tasks without trapped
navigation, unreadable or unreachable controls, persistent overlay obstruction,
or unusable camera/touch behavior. Attractive screenshots cannot establish
usability, and additional features cannot compensate for a broken core workflow.

### Additional features: up to 20 points

Award up to 5 points each for at most four distinct, useful features beyond this
edition's mandatory requirements: user value 2, completeness 1, coherent UI/UX
integration 1, and demonstrated correctness/reliability 1. Explain the evidence
for every award. Extra features are optional and their combined score is capped
at 20; an application meeting only the mandatory scope can earn up to 130/150.

Do not count mandatory features, cosmetic variants of one feature, raw catalog
quantity without added user value, or unfinished demonstrations as separate
extras. Optional extensions listed in this brief are eligible when delivered and
validated. Demonstrated offline support is one eligible extra where optional;
mandatory features never earn additional-feature points. All extras must
preserve scientific honesty, physical scale, source rights, and usability.
