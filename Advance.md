# Solar System Agent Build - Advance

Copyright (c)Terry Wan (starward-observatory.com) 2026

This notice applies to this brief. Submitted applications do not need to carry
Terry Wan's copyright notice; their authors retain ownership of their original
work, subject to applicable third-party rights and licenses.

## 1. Objective and starting material

Build an original browser observatory that combines a physically scaled Solar
System, a varied astronomical catalog, and practical Earth-based observing tools.
Choose and justify your own scientific models and implementation. This brief
does not prescribe methods, algorithms, frameworks, engines, or services.

Use this brief and the verification report example. Independently acquire lawful scientific data and
visual assets, retain provenance, and comply with source and license terms.
This is a standalone edition with reduced catalog, companion-tool, and acceptance
requirements relative to Challenge.md. Basic.md's prescribed method does not
apply. All requirements below are mandatory except section 7's optional features.

The [reference observatory](http://starward-observatory.com/) may be
explored through its visible interface and ordinary browser interactions.
Normal browser loading and rendering are allowed. Do not inspect, extract,
download for analysis, or reuse its source, bundles, network-response bodies,
data, or visual assets, including copies from repositories, mirrors, caches,
archives, or third parties. Screenshots may document behavior but must not
become copied interface or texture assets. Use an original identity without
implying endorsement or ownership of the reference's work.

## 2. Catalog and physical scene

Include the Sun, all eight major planets, at least 16 moons spanning Earth,
Mars, Jupiter, Saturn, Uranus, and Neptune, two dwarf planets, and two comets.
Include at least 500 sourced stars for orientation in the observing view.
Qualify illustrative appearance and label missing values as unavailable.

Use one documented physical scale for body sizes, positions, separations, and
rings. Keep screen markers separate from physical geometry. Show recognizable
bodies, sourced rotation periods and pole orientations where available, and
the ring systems of Jupiter, Saturn, Uranus, and Neptune. Disclose approximate
rotation or appearance. Illuminate bodies consistently from the Sun.

Provide body selection, camera focus/follow, rotate, pan, zoom, reset, labels,
orbit toggles, and an information panel with sourced dimensions, orbital or
rotation data when available, and source links.

## 3. Time and trajectories

The scene and observing controls cover all calendar years 2000-2050. Required
planets and moons must have usable modeled positions throughout this range.
Dwarf planets and comets may have narrower source coverage. Display those
limits and show unavailable positions explicitly. Label modeled estimates
and disclose their accuracy limits separately from the date range.

Provide pause, forward and reverse playback, speed selection, and direct UTC
date/time entry. A date jump must give the same result regardless of playback
history. Explain the selected models, reference frames, time conventions,
units, and the meaning of displayed orbit paths.

## 4. Earth observation and tonight planning

Let users select a site by city or latitude/longitude, choose a date, and view
geometric altitude and azimuth for the Moon and planets. Show the local
horizon and star context. Document the observer position, coordinate convention,
and treatment of parallax, light travel time, refraction, and terrain. Clearly
label approximations and distinguish observing directions from exterior scene
positions.

For one selected target, plot its altitude over the local night and highlight
sampled windows when it is above a stated altitude threshold and the Sun is
below a stated darkness threshold. Sampling at intervals of up to 30 minutes
is sufficient. State the time zone and resolve the night from local noon to
the next local noon. Label sampled windows as estimates, show empty or
unavailable results clearly, and disclose any location storage or transmission.

## 5. Scientific acceptance

Submit one short report with the tested application version, source links,
model assumptions, expected and observed results, and limitations. A readable
table is sufficient.

| Check | Required evidence |
| --- | --- |
| Positions | Compare Earth, one other planet, and Earth's Moon with an independent reference at three dates spread across 2000-2050. Match center, frame, time scale, and units, and report position differences and any material discrepancies |
| Date coverage | Jump to the first and last supported dates and to a date near the middle. Verify that required planets and moons have usable positions and that returning to the same date reproduces the same scene state |
| Physical scale | Check a planet radius, the Earth-Moon separation, and a ring radius against the declared scale |
| Observer directions | Compare altitude and azimuth for one planet and the Moon at a documented site and time with an independent reference. State the direction convention and report differences |
| Night planner | Verify one night with a usable window and one without. Check the displayed window against the sampled target altitude and darkness thresholds |

These checks establish representative behavior. Report observed differences
and limitations without claiming validated precision across the full range.

## 6. Operational acceptance and delivery

Submit a public URL to the runnable application and an agent-authored
`VERIFY.md`. The public URL must open the tested release without requiring an
account. Use [Verify-Report-Example.md](./Verify-Report-Example.md) as the report
structure and include the source and asset credits. Source code and build
archives are outside the submission.

Report a short walkthrough on one desktop browser and one mobile browser or
touch-emulated viewport. Identify the tested environments and whether the
mobile result used emulation. Demonstrate build and launch, body selection and
camera navigation, pause/reverse and date entry, one observing workflow, and a
clear response to one invalid input or unavailable data case. Record observed
failures and coverage gaps.

Core requirements are scored out of 100 points. Scientific correctness and
honest limits earn 30, catalog and feature completeness 25, interaction and
mobile usability 20, operational reliability 15, and reproducibility and
provenance 10. Prohibited copying, fabricated evidence, source/license
violations, or a broken primary experience prevent a passing submission.

## 7. Optional extensions

Spacecraft, artificial satellites, dedicated trajectory and Journey views,
constellations, deep-sky catalogs, size comparison, multi-target scheduling,
Moon-separation filters, observing exports, eclipse and event tools, Galactic
navigation, surface observers, offline support, and signed release packaging
are eligible as additional features when implemented and verified.

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
