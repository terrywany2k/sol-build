# Solar System Agent Build Challenge

Copyright (c) 2026 Terry Wan. All rights reserved.

This notice applies to this challenge document. Submitted applications do not
need to carry Terry Wan's copyright notice; their authors retain ownership of
their original work, subject to applicable third-party rights and licenses.

Build an original browser observatory that makes the Solar System understandable
at physical scale and connects exploration with practical sky observation.
Deliver a working application, independently acquired scientific and visual
sources, a downloadable distribution, and evidence for its stated capabilities.

This is a product and acceptance specification. It does not prescribe a
framework, engine, programming language, algorithm, service, or development tool.
All requirements are mandatory unless explicitly marked Bonus.

## Reference boundary

You may inspect [the reference observatory](https://starward-observatory.pages.dev/)
through its visible interface and ordinary browser interactions to understand
the requested experience. Normal browser loading and rendering are allowed.

Do not inspect, extract, download for analysis, or reuse its HTML source,
JavaScript bundles, stylesheets, application data, network-response bodies,
catalogs, images, textures, models, or other implementation assets. Do not use
DevTools or network inspection to recover its implementation or data. Do not
obtain equivalent copies through repositories, mirrors, source caches, archives,
or third parties. Screenshots may document observed behavior, not become copied
interface or texture assets.

No source code, scientific datasets, images, or models are supplied with this
challenge. Acquire your own lawful sources independently of the reference,
retain provenance and comply with their terms. An original name and visual
identity are welcome. Exact pixel copying, implied endorsement, and ownership
claims over the reference's branding or work are not part of the challenge.

## 1. Catalog and physical scene

Provide at least this independently sourced baseline:

| Category | Minimum breadth |
| --- | --- |
| Natural bodies | 74: Sun, eight major planets, five dwarf planets, 37 moons and 23 comets |
| Moon systems | Earth, Mars, Jupiter, Saturn, Uranus and Neptune represented |
| Comets | Periodic and unbound objects, with at least six source-backed time-varying trajectories |
| Spacecraft | 39 mission entries, spanning multiple destinations and mission eras |
| Artificial Earth satellites | 24 entries spanning low, medium, geostationary and highly elliptical orbits |
| Sky | At least 8,000 catalog stars, 88 constellations and 100 identified deep-sky targets |
| Landmarks | At least 40 coordinate-bearing features across at least eight solid worlds |

Exact catalog identities need not match the reference. Substitutions must retain
comparable breadth and genuine coverage. One example per category is not a
complete submission. Missing measurements remain unavailable; do not invent
them to meet counts. Distinguish physical centers from system barycenters.

In the ordinary 3D scene, positions, radii, moon separations and ring dimensions
share one documented physical length scale. Camera navigation must bridge the
large difference between meter-scale spacecraft and planetary distances.
Spacecraft meshes use source-backed meter dimensions or explicitly identified
approximate representations, never a minimum kilometer-size boost. Screen
markers and labels may remain readable at fixed pixel size if clearly separate
from physical geometry. Unknown size does not silently become a physical radius.

Support selection, search, focus, parent-centered orbit framing, following,
rotation, zoom, pan, labels, orbit layers and a size-comparison view. Compare
planets and at least 20 moons at one body-size scale, explaining any compressed
spacing. Include rings, qualified irregular shapes and honest illustrative maps
where measured surfaces are unavailable. Add a navigable Galactic context and
a reversible transition back to the Solar System.

## 2. Time, dossiers and journeys

The scene accepts dates throughout 1900-2200; observing tools accept 1900-2100.
Model-specific coverage can be narrower and must be enforced visibly. Provide
pause, forward/reverse playback, rate selection, precise date entry and UTC,
local-time and TT presentation without changing the represented instant.
Unavailability, approximation and prediction must not look like observations.

Keep simultaneous geometric positions in the exterior scene distinct from
Earth-observer light-time-corrected directions. Model and explain applicable
observer parallax, reference frames and receiving/emission epochs. Do not
silently reuse one convention for both purposes.

Natural-body and artificial-object dossiers include sourced descriptions,
orbital information, current coordinates, chronological milestones, photographs
or qualified models, source links and availability. Keep dossiers readable while
time changes. After Orbital information, provide independent inline sections:

- An Earth map showing where the target center is above the sea-level geometric
  horizon, with finite-distance parallax, independent Sun-below-horizon shading,
  a subtarget marker and the selected site. State that this is not detectability.
- A 50-degree nearby-star chart in fixed J2000, north up and east left, centered
  on the selected site's direction or an explicitly labeled geocentric fallback.
  Include magnitude selection and existing catalog constellation connections.
- For comets, an interactive 3D snapshot containing only point symbols for the
  Sun, eight planets, Pluto and the selected comet, plus orbit lines. Use common
  AU coordinates, a supported partial comet arc, and date/time markers for the
  snapshot position, modeled perihelion and the same return's closest Earth
  approach. Distinguish model minima from published event clocks. Missing events
  stay unavailable. Planet ellipses are reference curves, not historical tracks.

The comet preview supports rotate, zoom and reset; it makes no full-orbit or
extrapolation promise. Any photographic Milky Way backdrop must be independently
licensed, visibly credited and described as illustrative if not astrometrically
aligned. It must not alter orbit coordinates.

Provide bounded comet/mission milestone playback and spacecraft Journey views.
A Journey camera follows the evaluated physical trajectory, with free look,
field-of-view zoom, source quality, UTC, heliocentric speed and Sun/Earth distance.
Show target center distance, nearest supported ellipsoid-surface clearance,
angular extent and signed radial approach speed with distinct meanings.
Do not infer attitude, thrust or terrain clearance. Hold or stop at unavailable
data and coverage boundaries. Leaving restores the prior scene and clock;
superseded asynchronous work cannot restore an obsolete session.

## 3. Surface and Earth observation

Provide a landmark atlas with real coordinate conventions, photographs, sources
and qualified image placement. Physical latitude/longitude must remain distinct
from annotation pixels. On supported solid worlds, allow a surface observer
2 m above a reference ellipsoid, local free look, editable site and an analytic
geometric horizon. Reject unsupported physical centers and surfaces explicitly.
Return restores the preceding scene and landmark selection.

Surface ground may reuse a registered global map with subtle illustrative
detail and sunlight shading. It must not imply local measured terrain. Disclose
omitted atmospheric scattering, refraction and terrain, particularly for Venus
and Titan. Preserve observer-specific receiving/emission geometry.

Earth telescope mode supports cities, manual coordinates, time zones, tracking,
local altitude/azimuth, equatorial readouts, angular zoom and optical orientation
controls. Sky layers include stars, constellations, deep-sky imagery and pins.
Deep-sky mode starts off, hides Solar System content when enabled, supports
clickable targets and pin/unpin, and offers fine pan controls including WASD.
Constellation details expose member links and source-qualified information.

## 4. Planning and companion tools

Provide all of the following with explained approximation limits:

- Tonight target curves and usable windows, using local noon to next local noon.
- A rolling selected civil date plus the following 30 dates: 31 night starts,
  crossing month/year boundaries and resolving each local noon separately.
- Target ranking, darkness/altitude/Moon constraints and a custom azimuth horizon.
- A multi-target night plan with duration, priority and setup/transition costs,
  explanations for unscheduled targets, and calendar export.
- Solar/lunar eclipse search, local circumstances and interactive eclipse replay.
- Transit demonstrations, retrograde motion and a satellite-event theatre
  covering at least ten moons in multiple planetary systems, with honest
  event-support and source-coverage limits.
- A manual star finder, interactive star-hop chart, local observing logbook,
  equipment records and eyepiece-field reference.
- Angular/distance measurements, saved views, shareable links and useful image
  or data exports that preserve the represented date and observing context.
- A separate natal-chart workspace with four explicitly named house systems,
  local privacy controls and honest polar-latitude unavailability. Never silently
  substitute a different house system. Present astrology separately from science.

Default planning sampling must be no coarser than 10 minutes on ordinary nights;
disclose any justified exceptional coarsening. Sampling is not exact rise/set
or a weather, brightness or equipment-detection prediction. Preserve DST nights,
ambiguous local-time policy, skipped civil dates, and unavailable source windows.

## 5. Scientific acceptance

Publish a machine-readable result table and a readable explanation. Every
reference comparison identifies source/version, target and center IDs, units,
frame, time scale, epoch, coverage and the exact application candidate.
Independent validation epochs must not be training/fitting samples. Keep those
holdouts identifiable and report all failures, not only favorable witnesses.

| Mandatory check | Acceptance gate |
| --- | --- |
| Planetary states | Earth, Moon and all eight planets: at least 100 independent epochs per target spanning the declared qualified interval, including endpoints and multiple eras |
| Planetary position agreement | Planets: maximum Cartesian residual <= 1,000 km and <= 0.01% of reference distance; Moon relative to Earth: <= 100 km and <= 0.05% |
| Additional natural bodies | At least six moons across two systems and six comets, each with >= 50 independent epochs; maximum residual <= 100 km and <= 0.1% in the stated comparison frame |
| Artificial objects | At least six spacecraft and six satellites compared at >= 20 source-covered epochs each; state explicit finite validity, model class and measured maximum errors |
| Event clocks | At least 30 independently published clocks across solar eclipses, lunar eclipses, oppositions and lunar phases; <= 60 seconds maximum absolute difference under matched definitions |
| Physical scale | Numerical dimension and distance checks for every rendered category, plus a meter-scale spacecraft against a planet without an individual mesh enlargement |
| Observer geometry | Independent direction/parallax cases, including the Moon near the horizon, an ellipsoid surface site, receiving/emission epoch handling and a daylight/night boundary |

For every position cohort report maximum absolute error, RMS, and percentage
error, with the epoch and reference distance for each maximum witness.
Define percentage as `100 * norm(model-reference) / norm(reference)` in the
declared center-relative frame. Treat zero denominators explicitly. An average
cannot conceal a failed maximum. Additional approximate bodies still require
reported evidence and honest labels; they do not inherit the qualified cohort's
accuracy. Finite sampled agreement is not a continuous or physical uncertainty
bound, nor a claim that all objects are accurate for all three centuries.

Event comparisons must match physical versus received time, geocentric versus
site location, contact/maximum definition, shadow standard, time scale and
published precision. Preserve differing-definition comparisons separately;
do not call a standards difference a software error or shift source clocks to
manufacture agreement. Unqualified event families remain explicitly approximate.

Catalog photometry retains source passbands, quality and missingness. Finite
negative B-V and zero magnitudes are valid data. Do not invent temperatures,
radius, distance or colors as measured facts. Artistic stellar activity and
surface reconstructions require clear qualifiers.

## 6. Operational acceptance

Provide observed pass/fail results for these scenarios on desktop Chrome and
Safari, iOS Safari and an Android-class Chrome viewport/device. Identify actual
devices separately from emulation; emulation alone cannot certify iOS support.

| Scenario | Required outcome |
| --- | --- |
| Cold load, reload and warm cache | Reach a usable scene without hidden initialization failures; report readiness time, request count, transfer bytes and device/network conditions |
| Desktop and constrained loading | Demonstrate bounded desktop preload readiness and mobile lazy loading; avoid unbounded serial request chains or timeout-driven initialization |
| Failure and retry | Exercise unavailable source intervals, a real 404, corrupt/hash-mismatched input and retry; show a useful state without fake data or stale publication |
| Repeated navigation | At least 25 dossier/view open-close-switch cycles, including rapid cancellation, with no accumulating owned contexts/listeners/timers or stale updates |
| Clock and calendar | Pause/reverse/boundary playback, inclusive date ranges, DST 23/25-hour nights, month/year rollover and invalid/skipped local dates behave as declared |
| Interaction | Keyboard, focus return, modal dismissal, touch rotate/pinch, whole-panel mobile scrolling and minimized controls remain usable |
| Geometry | Solar partial/total/annular occlusion, near-surface horizon, polar/seam maps and large solar closeups have no false silhouette gaps or stretched sampling artifacts |

Report transfer, decoded-memory and GPU/resource budgets, and demonstrate stable
interaction on the named mobile target. Unsupported browser results are gaps,
not passes. Geolocation and native saving must describe their real secure-origin
and permission requirements; do not claim a capability works over plain HTTP
without testing that environment.

The distribution must work from a documented static-host subpath. Offline after
first load is Bonus, and only the explicitly demonstrated cached scope may be
claimed; it must not imply every date, image or trajectory is available offline.
Privacy-sensitive location, logbook and birth data must have clear storage,
export and deletion behavior without undisclosed transmission.

## 7. Deliverables and scoring

Deliver complete source, locked dependency versions, original identity, build
instructions, source/asset credits and licenses, the scientific and operational
results, and a working static distribution with downloadable `dist.zip`.
Record retained source inputs and reproducible provenance. Exclude secrets,
private keys, private records and unnecessary authoring files from the public ZIP.

A release must include a file inventory, integrity hashes and an authenticity
check backed by a separately trusted public key. State the trust boundary:
replacing both application and embedded verifier can defeat a same-origin check.
Keep signing secrets outside the public package. Obfuscation is not proof of
authenticity, confidentiality or impossible-to-bypass anti-tampering.

Core requirements are scored out of 100 points: scientific correctness and honest limits
30; feature completeness 30; interaction/mobile accessibility 20; operational
robustness 10; reproducibility, provenance and packaging 10. Offline support is eligible for the additional-feature score below and cannot
replace mandatory work.

Hard failures are copying prohibited reference implementation/assets, scientific
misrepresentation or fabricated results, undisclosed source/license violations,
and a broken primary mobile experience. An attractive rendering cannot offset
these failures. A successful submission is independently built, demonstrably
usable, and precise about what its evidence does and does not establish.

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
