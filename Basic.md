# Solar System Agent Build - Basic

Copyright (c) 2026 Terry Wan. All rights reserved.

This notice applies to this brief. Submitted applications do not need to carry
Terry Wan's copyright notice; their authors retain ownership of their original
work, subject to applicable third-party rights and licenses.

## 1. Objective and starting material

Build an original browser-based 3D Solar System using fixed-element elliptic
Kepler propagation and correct physical proportions. The result must be a
coherent, broadly correct Solar System: revolution, axial tilt, physical spin,
major moons, rings, appearance, and illumination are core requirements.

Only this brief is provided. Independently acquire lawful orbital elements,
physical dimensions, and any visual assets. Record sources, epochs, units,
licenses, and approximation limits. Choose your own language, framework, engine,
and visual identity. This is a standalone edition; requirements from Advance.md
and Challenge.md do not apply.

The [reference observatory](https://starward-observatory.pages.dev/) may be
explored through its visible interface and ordinary browser interactions.
Normal browser loading and rendering are allowed. Do not inspect, extract,
download for analysis, or reuse its source, bundles, network-response bodies,
data, or visual assets, including copies from repositories, mirrors, caches,
archives, or third parties. Screenshots may document behavior but must not
become copied interface or texture assets.

All requirements below are mandatory except the optional extensions in section 7.

## 2. Bodies and physical scale

- Include the Sun, all eight major planets, and these 16 moons: Earth's Moon;
  Phobos and Deimos; Io, Europa, Ganymede, and Callisto; Titan, Rhea, Iapetus,
  and Enceladus; Titania, Oberon, and Miranda; Triton and Nereid.
- Use one documented physical length scale for body radii, orbital distances,
  moon separations, and rings. Preserve both body-size ratios and the ratio
  between body sizes and distances. Do not enlarge individual bodies or compress
  the ordinary scene's orbital distances to make them visible.
- Keep small or distant bodies selectable with clearly separate screen markers,
  labels, and list entries. Camera focus must make true-scale bodies inspectable.
- Provide a size-comparison view for the eight planets, using one radius scale.
  Bodies may be rearranged there if the spacing is explicitly non-orbital.
- Use sourced dimensions and recognizable, source-informed appearance, including
  major surface or atmospheric features. Do not use one generic appearance for
  every body. Textures or procedural materials are acceptable; qualify inferred
  or illustrative details and unavailable surface maps.

## 3. Orbital model

Use independently sourced elliptic orbital elements with declared epochs and
parent bodies. Keep semi-major axis, eccentricity, inclination, ascending node,
and argument of periapsis fixed. Advance mean anomaly from its epoch using the
sourced period or a consistently derived mean motion, then solve Kepler's
equation `M = E - e * sin(E)` to obtain each orbit's position.

Apply the complete three-dimensional orbital orientation. Preserve retrograde
geometry where applicable, including Triton's retrograde orbit. Each moon's
vector is relative to its parent; transform it from its declared source frame
into the common scene frame before adding the parent's position. Do not assume
every moon's source elements use the same reference plane. Keep the Sun at the
origin and document a consistent
right-handed rendering frame, angle units, and length conversions.

Compute positions directly from the selected instant so that date jumps and
reverse playback do not depend on animation history. Use a declared uniform
time scale for propagation and UTC for input/display; explain the conversion
and any approximation. Bound the solver's iterations and handle unsupported
elements or non-convergence explicitly.

Support every valid UTC date/time throughout calendar years 1900-2200, from
1900-01-01T00:00:00Z inclusive to 2201-01-01T00:00:00Z exclusive. This is the
mandatory operating range for all required bodies, not a minimum duration that
participants may replace with a chosen one-year or source-centered interval.
Direct date entry, orbital evaluation, physical spin, and forward/reverse
playback must work throughout this range without requiring precomputed frames.
At either boundary, stop playback at a valid boundary instant with a clear
message; do not silently wrap, reset, or substitute another date.

Distinguish the application's operating range from the model's scientific
accuracy. Fixed elements are an educational approximation, and errors can grow
far from their reference epoch. Explain the source epoch and these limits
visibly, while still evaluating the declared fixed-element model throughout
1900-2200. Do not shorten the required operating range because a source only
qualifies higher accuracy near its epoch, and do not claim precision ephemerides
or uniform astronomical accuracy across three centuries. Choose source inputs
that can lawfully support this explicitly approximate use; do not violate their
terms or present model extrapolation as a source-provided observation.

Physical spin must be modeled separately from orbital revolution, with
independent periods and directions.

## 4. Spin, rings, and illumination

Give the Sun, planets, and moons physical rotation based on sourced periods,
pole orientation or axial tilt, and a declared reference phase. Explain the
reference plane and sign convention. Preserve the unusual orientations and
retrograde rotation of Venus and Uranus; never make every body spin the same
way or once per orbit by default. A declared rigid-rotation approximation for
the Sun and giant-planet atmospheres is sufficient.

Use a sourced or explicitly qualified orientation for synchronously rotating
moons. Earth's Moon and other known synchronous moons should approximately keep
the same face toward their primary, with a documented policy for eccentricity,
libration, and tilt. Do not force unrelated bodies into tidal locking. Where
rotation measurements are incomplete, disclose a supported approximation or
unknown value rather than silently claiming an invented period or pole.

Render the ring systems of Jupiter, Saturn, Uranus, and Neptune. Use sourced
inner/outer dimensions and orient each ring system in its planet's equatorial
plane so that it follows the physical pole rather than the camera. Include
Saturn's recognizable main ring structure and gaps; qualify simplified faint
rings or arcs. Rings must surround rather than fill the planet, preserve physical
proportions, and occlude correctly when seen from above, below, or edge-on.

Illuminate bodies from the Sun with consistent day/night sides and phase
geometry. The Sun is luminous, and nearby moons must not have arbitrary light
directions. Show the principal atmospheric appearance of Earth, Venus, and the
giant planets, plus Earth's cloud layer. Keep cloud and atmosphere shells near
their sourced physical extent; qualify approximations without changing the
body's physical radius. Full atmospheric scattering, cast shadows, and precise
eclipse rendering are optional, but basic lighting must not imply they exist
when they are absent.

Spin, orbit, cloud animation, and ring orientation must respond consistently to
the selected simulated instant, including pause, reverse, and direct date jumps.
Document texture registration and any unknown prime-meridian phase; do not
present an arbitrary texture alignment as a measured orientation.

## 5. Interaction and delivery

Provide orbit, pan, zoom, reset, body selection, camera focus/follow, labels,
orbit-path toggles, pause/resume, forward/reverse speeds, UTC date/time entry,
and a visible simulated clock. Pausing must preserve camera interaction.

Show a concise information panel with sourced dimensions, orbital and rotation
periods, axial tilt or pole orientation, parent, current model coordinates,
units, and source links. Orbit paths must
agree with the moving bodies' fixed orbital geometry.

Support usable desktop mouse/keyboard controls and mobile touch controls.
Provide helpful loading and failure states. Deliver complete source, locked
dependencies, documented install/build/serve commands, and a static production
build that loads its data through HTTP. Include a short English explanation of
the model, scale, coordinate/time conventions, sources, and known limitations.

## 6. Acceptance and scoring

Publish the checks actually performed, their inputs, expected results, observed
results, and the exact application version. A concise table and explanation are
sufficient; this edition does not require Challenge's ephemeris error gates.

| Check | Required evidence |
| --- | --- |
| Catalog and scale | All 25 required bodies; numerical radius and distance checks against the declared common scale, including Earth-Moon separation and all four ring systems |
| Kepler solver | A circular case and at least two nonzero-eccentricity cases, with residuals meeting a stated numerical tolerance and bounded convergence |
| Orbital geometry | Periapsis/apoapsis distances, return after one period within stated floating-point tolerance, and a nonzero-inclination case |
| Time and parents | Repeatable date jumps, pause/reverse behavior, source-frame conversion, and parent-plus-moon composition across all six moon systems |
| Mandatory date range | All required bodies evaluate to finite positions and orientations at at least 12 dates distributed across 1900-2200, including the first instant, the last supported instant at the application's stated time resolution, and dates in 1900, 1950, 2000, 2050, 2100, 2150, and 2200; exercise actual date-entry and playback controls as well as model calculations |
| Calendar and boundaries | Accept 2000-02-29; reject 1900-02-29 and 2100-02-29; handle year rollover and both playback boundaries without silent date substitution; revisit a date after jumping across centuries and obtain the same position and spin |
| Spin and poles | Rotation period and direction checks, a full-turn return within stated numerical tolerance, Venus/Uranus orientation, approximate synchronous facing, and consistent date jumps |
| Rings | Sourced radial dimensions, pole alignment, recognizable Saturn structure, and correct front/back/edge-on visibility for all four systems |
| Appearance and lighting | Recognizable bodies, Earth clouds, declared atmospheric extent, and Sun-relative illumination/phase checks from multiple camera directions |
| Interaction | Body selection and focus at physical scale, camera use while paused, and working size comparison |
| Delivery | Observed build and browser startup, reload, and a missing-data or missing-asset case |
| Devices | At least one named desktop browser and one mobile browser or touch emulation, clearly distinguishing emulation from a real device |

External astronomical spot comparisons are welcome, but must disclose the
fixed-element model's differences rather than substitute visual agreement for
numerical checks. Report untested environments and failures honestly.

Core requirements are scored out of 100 points: Kepler model and orbital geometry 25; physical
scale and catalog 20; spin, rings, appearance, and illumination 25; interaction
and usability 15; reproducibility, validation, and sources 15. Missing mandatory
features, incorrect physical proportions, prohibited reference copying, or
fabricated evidence prevent a passing submission. Visual polish does not excuse
incorrect revolution, spin, ring geometry, or parent relationships.

## 7. Optional extensions

Additional moons and dwarf planets, elliptic comets, catalog stars, detailed
shadows and eclipses, richer surface detail, saved views, and image/data export
are welcome.
Keep every addition consistent with the physical scale and its declared model.
Extensions do not replace the required bodies, controls, or checks.

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
