# Build Challenge: Recreate the Solar System

## 1. Purpose

Build a complete browser-based 3D Solar System from scratch.

The implementing Agent is given only this file and the following two directories:

```text
Build.md
data/
images/
```

No original source code, stylesheet, HTML, tests, package manifest, build script, screenshots, or other project documentation is available. The goal is not to reproduce a hidden codebase line for line. The goal is to measure how much of a correct, polished, data-driven astronomical visualization an Agent can independently design and implement from this specification.

Treat `data/` as the authoritative model and `images/` as the supplied visual asset library. Do not invent replacement orbital elements for records that already exist. Do not modify the supplied JSON or image files merely to make the implementation easier.

## 2. Challenge contract

### 2.1 Allowed

- Create any source files, tests, configuration, and build tooling needed by the application.
- Use JavaScript or TypeScript and any sensible browser rendering framework. Three.js is recommended, but not mandatory.
- Add stable open-source dependencies when they materially help the implementation.
- Generate procedural geometry, shaders, labels, controls, and UI assets in code.
- Derive indexes, normalized records, and runtime caches from the supplied data.
- Choose an original visual design. Exact pixel matching is not expected.

### 2.2 Not allowed

- Recover, search for, copy, or infer from the original project source repository.
- Fetch a second ephemeris and replace the supplied orbital model with it.
- silently ignore malformed records or change scientific fields in `data/`.
- Hard-code a separate body list that can drift away from `data/datasource.json`.
- Require a private service, secret, paid API, or server-side database to run.
- Claim observatory-grade accuracy. This is a deterministic visualization model, not SPICE, Horizons, SOFA, or a full N-body ephemeris.

### 2.3 Expected result

The result must be a self-contained web project that can be installed, tested, built, and served locally. A reviewer should be able to run commands documented by the Agent and open the simulation in a current desktop browser.

At minimum, the project must provide:

- A clear setup section in its own README.
- A deterministic production build.
- A local development command.
- Automated tests for the orbital solver and data boundary.
- A graceful on-screen error if required data or WebGL initialization fails.
- No `file://` requirement; JSON must be loaded through HTTP.

The implementation should not depend on PHP. A static production build is preferred.

### 2.4 Reference demo and copyright

An existing demonstration page is available at:

[https://solar-a7l.pages.dev/](https://solar-a7l.pages.dev/)

The implementing Agent may use this page as a behavioral and visual reference to understand the intended product experience. It may observe the rendered result and interact with the public UI, but it must not copy, download, reverse-engineer, or recover the demo's original source code. The new implementation should satisfy this specification in its own architecture and does not need to be a pixel-perfect clone.

The finished application must visibly include the following attribution in an About panel, footer, information panel, or another reasonably discoverable location:

```text
Copyright Terry Wan
```

Do not remove, obscure, rename, or replace this attribution. The Agent may add its own implementation credit separately, but must not imply ownership of Terry Wan's supplied data, images, project concept, or original work.

## 3. Supplied assets and data

The current snapshot contains:

- 58 orbiting body records: 8 planets, 5 dwarf planets, 37 moons, and 8 comets.
- A separate Sun record.
- 8,356 base stars and 38,788 ultra-faint stars.
- 674 deep-sky/nebula records and 674 corresponding nebula images.
- All 88 IAU constellations: 12 zodiac groups and 76 other groups.
- 85 constellation artwork records and images.
- 637 observing locations grouped under 160 country/region keys.
- Reference position samples for the eight planets.
- 831 image files in total at the time of writing.

Counts are a description of this snapshot, not a schema invariant. The application must derive its actual menus and counts from the files at runtime.

### 3.1 Files

| File | Required use |
| --- | --- |
| `data/datasource.json` | Primary body, correction, spin, J2, and project metadata. Required for boot. |
| `data/skybox_star.json` | Base star catalog and deep-sky catalog. The Solar System must still boot if this optional sky layer fails. |
| `data/skybox_star_ultrafaint.json` | Additional faint stars. Load on capable desktop devices; it may be skipped on mobile. |
| `data/constellations.json` | Constellation polylines, localized names, and image anchors. |
| `data/cities.json` | Telescope/observer locations. |
| `data/validate.json` | Heliocentric ecliptic reference positions in AU for diagnostics. |
| `images/` | Body textures, ring textures, constellation artwork, nebula artwork, and star-related assets. |

### 3.2 Asset paths

Body image fields such as `texture_hint`, `texture_nightmap`, `texture_normal_map`, `texture_specular_map`, `texture_atmosphere`, and `texture_ring` are paths relative to `images/`.

Constellation image records use paths such as `constellations/aquila.png`, also relative to `images/`.

Nebula records use an image filename such as `m1dumont.png`; resolve these below `images/nebulae/`.

Texture lookup must be data-driven. Missing optional textures should produce a reasonable fallback material and a diagnostic warning, not a fatal boot failure.

## 4. Product requirements

### 4.1 Core experience

The first usable view should show a textured Sun, orbiting bodies, orbit paths, a star background, and camera controls. The user must be able to understand that this is a time-driven model rather than a static illustration.

Required controls:

- Orbit, pan, and zoom camera controls.
- Select a planet, dwarf planet, moon, comet, or Sun from a generated list.
- Click or tap visible major bodies to select them.
- Smoothly focus the camera on the selected object without breaking its continued orbital motion.
- Pause/resume simulation time.
- Change time speed in both forward and reverse directions over a wide range.
- Jump to a user-entered UTC date and time.
- Snap to the current time.
- Reset to a Solar System overview.
- Toggle labels, orbit lines, and selection halo.
- Toggle orbit categories independently: planets, dwarf planets, moons, and comets.
- Display selected-object information derived from its JSON record.
- Display current simulated UTC, TT day offset from J2000, Julian Date, and current speed.

The interface must be usable with mouse and touch, responsive at narrow widths, keyboard accessible where practical, and visually legible over the 3D scene.

### 4.2 Scene contents

Required:

- Sun at the origin.
- Every valid planet and dwarf-planet record orbiting its declared primary.
- Every valid moon attached to its declared primary.
- Every valid comet, including high-eccentricity Halley, with a visible head and orbit.
- Textured spherical surfaces using supplied assets.
- Planetary rings wherever `texture_ring` exists.
- Atmosphere/cloud shell wherever `texture_atmosphere` exists.
- Orbit lines that use the same current orbital plane as the moving body.
- Labels and a visible selected-object indicator.
- Background stars placed from the catalog rather than randomly generated in place of it.

Strongly recommended:

- A comet tail oriented approximately away from the Sun.
- Sun glow.
- Earth day, night, normal, specular, and cloud maps.
- A base-lighting mode for readability and a phase-lighting mode emphasizing the solar terminator.
- Shadows where performance permits.
- A subtle ecliptic/AU grid.
- An automated tour of bodies.

### 4.3 Visual scale

Real radii are far too small relative to interplanetary distance for a useful single-view visualization. Preserve correct orbital distance ratios, but it is acceptable to exaggerate display radii or apply a documented minimum visible radius.

A known useful linear scale is:

```text
AU_KM = 149597870.7
world units per km = 0.000001 * 6
world units per AU = AU_KM * 0.000001 * 6
```

This exact scale is not mandatory. Whatever scale is chosen must be centralized, applied consistently to planets and moon systems, and documented. Dwarf planets and comet nuclei may use a minimum display size, but information panels must report physical `radius_km`, not the exaggerated display radius.

## 5. Data loading and normalization

### 5.1 Boot sequence

Implement a visible loading state and use this order:

1. Initialize the renderer, scenes, camera, controls, and basic UI.
2. Fetch and validate `data/datasource.json`.
3. Fetch independent sidecars concurrently.
4. Normalize missing optional top-level sections to empty objects or arrays.
5. Build name indexes before resolving moons and selections.
6. Install correction tables.
7. Create the Sun, planets/dwarfs, moons, and comets.
8. Install sky and constellation layers.
9. Start animation only after the minimum scene is coherent.
10. Remove the loading overlay; retain a useful retry path on fatal failure.

Failure of the primary datasource is fatal. Failure of ultra-faint stars, validation data, cities, constellations, or nebula artwork is non-fatal and should disable only the affected feature.

### 5.2 Primary model shape

`data/datasource.json` contains these relevant roots:

```text
meta
sun
bodies[]
corrections.encke_kick
corrections.secular_terms
corrections.periodic_terms
j2
```

Do not assume empty constellation or sky objects embedded in the primary file contain the real sidecar content. Load the dedicated sidecars.

### 5.3 Body records

The `type` field currently uses:

```text
planet
dwarf_planet
moon
comet
```

Common required orbital fields are:

| Field | Meaning |
| --- | --- |
| `name` | Unique display and lookup name. |
| `primary` | Parent body, usually `Sun` or a planet name. |
| `a_AU` | Heliocentric semi-major axis for planets, dwarfs, and comets. |
| `a_km` | Planet-centered semi-major axis for moons. |
| `e` | Eccentricity. The active model supports only `0 <= e < 1`. |
| `i_deg` | Inclination in degrees. |
| `Omega_deg` | Longitude of ascending node in degrees. |
| `omega_deg` | Argument of periapsis in degrees. |
| `M_deg` | Mean anomaly at J2000 in degrees. |
| `period_days` | Orbital period in days. |
| `retrograde` | Orbit-direction metadata; do not use it to negate mean motion when the supplied elements already define the orbit. |
| `frame` | Reference frame description. |

Physical and visual fields include `radius_km`, `radii_km`, `texture_*`, `axial_tilt_deg`, `pole_RA_deg`, `pole_Dec_deg`, `W0_deg`, `Wdot_deg_per_day`, `sidereal_day_hours`, `spin_direction`, and `spin_phase_deg`.

Validate finite numeric fields at the data boundary. Reject or skip an invalid individual orbit with a visible diagnostic, but do not let one optional body prevent all valid bodies from rendering.

### 5.4 Reference planes

Most common propagation records use `ecliptic_J2000`. Some moon records can describe a planet-equatorial J2000 frame. A robust implementation should attach a planet-equatorial orbit beneath the host's pole-alignment node, while ecliptic moon orbits should remain in the common ecliptic orientation.

Do not silently treat arbitrary planet-equatorial elements as heliocentric ecliptic elements. If a frame is unknown, report it and use a documented fallback.

## 6. Coordinates and scene graph

### 6.1 Source frame

Orbital calculations use the right-handed ECLIPTIC/J2000 frame:

- `+X_ecl`: J2000 mean vernal equinox.
- `+Y_ecl`: ecliptic plane, 90 degrees east of `+X_ecl`.
- `+Z_ecl`: ecliptic north.

### 6.2 Render frame

Use world `+Y` as up while preserving a right-handed frame:

```text
(x, y, z)_world = (x, z, -y)_ecliptic
```

Therefore world `+Y` is ecliptic north. Use this signed conversion everywhere: bodies, orbit lines, poles, stars, reference markers, and diagnostics. A missing minus sign mirrors the Solar System and is a correctness failure.

### 6.3 Recommended per-body hierarchy

```text
orbit/position node
└── body position node
    └── tilt node          local +Y aligned to the physical pole
        ├── spin node      absolute rotation around local +Y
        │   ├── surface
        │   └── atmosphere
        ├── ring mesh      fixed in the equatorial plane
        └── moon system nodes as appropriate for their frame
```

Orbit lines should not be children of a node whose current body position would translate them away from their primary.

## 7. Time model

### 7.1 Epoch and scales

```text
J2000.0 = JD 2451545.0
simDaysTT = JD_TT - 2451545.0
TT - UTC = approximately 69.184 seconds for this visualization
TT - UT1 = approximately 69.184 seconds for Earth rotation
one Julian century = 36525 days
```

Use TT days for orbital propagation. UTC is an input/display scale. The project does not model TDB separately.

For a JavaScript time in Unix milliseconds:

```text
JD_UTC = unixMilliseconds / 86400000 + 2440587.5
JD_TT  = JD_UTC + 69.184 / 86400
simDaysTT = JD_TT - 2451545.0
```

The fixed offset is intentionally approximate. State that no live leap-second table, EOP, polar motion, precession-nutation, or live UT1 feed is used.

### 7.2 Animation semantics

Simulation speed is simulated TT days per real second. Time must be accumulated independently of frame rate. Pause must freeze simulation time without freezing camera interaction.

All body positions and spins must be functions of absolute simulation time. Do not integrate rotations only with `rotation += rate * frameDelta`; that accumulates drift and produces inconsistent results after date jumps. An absolute jump must produce the same scene state regardless of the path used to reach that date.

After any absolute date jump or correction-toggle change:

- Recompute current body positions.
- Recompute absolute spins.
- Restore tidal locks geometrically.
- Rebuild orbit-line geometry when its plane depends on time-varying corrections.
- Keep the selected object and camera focus valid.

## 8. Elliptic orbital propagation

### 8.1 Scope

Implement one production Kepler solver for elliptic orbits only. Every supplied active orbit has `0 <= e < 1`. Do not silently apply the elliptic solver to parabolic or hyperbolic input.

### 8.2 Mean anomaly

For a record at TT day offset `t`:

```text
M0 = radians(M_deg)
n  = 2*pi / period_days
M(t) = M0 + n*t + correction_dM
```

Keep `M(t)` unwrapped so motion remains continuous across turns. Reduce only a temporary local copy when solving or evaluating trigonometric functions.

### 8.3 Safeguarded `solveE`

Solve:

```text
E - e*sin(E) = M
```

Required properties:

- Input domain is finite `M` and `0 <= e < 1`; invalid input returns/throws a clear invalid result.
- Circular orbits return `E = M` within floating-point precision.
- Preserve full turns: localize `M` to approximately `[-pi, pi]`, solve locally, then restore the removed turns.
- Use Newton iterations on the fast path.
- Maintain a monotonic bracket around the correct local root.
- Accept a Newton candidate only if finite and strictly inside the bracket; otherwise bisect.
- Use a symmetric high-eccentricity starter. Negative and positive local anomalies must be handled as mirror cases; a useful distance is `pi - abs(m)`.
- Use a bounded bisection fallback after the Newton budget.
- Target residual `abs(E - e*sin(E) - M) <= 1e-12` for normal finite inputs.
- Never jump to a different root branch while `M` moves monotonically, including Halley's negative half-cycle.

The solver must be tested at least for:

```text
e = 0, 0.1, 0.8, 0.96794279, 0.999999999
M over negative and positive values spanning at least 40 full turns
values very close to 0, +pi, -pi, and turn boundaries
```

### 8.4 Ellipse position

After solving `E`, use a reduced equivalent angle only for `sin` and `cos`:

```text
r = a * (1 - e*cos(E))
cos(nu) = (cos(E) - e) / (1 - e*cos(E))
sin(nu) = sqrt(1 - e*e) * sin(E) / (1 - e*cos(E))
```

Guard the denominator against floating-point collapse near periapsis. Build the position from the current unit basis vectors:

```text
position_world = P_world * (r*cos(nu)) + Q_world * (r*sin(nu))
```

### 8.5 Orbital basis

For `Omega`, `i`, and `omega` in radians, first construct the two in-plane unit vectors in ecliptic coordinates:

```text
P_ecl.x = cos(Omega)*cos(omega) - sin(Omega)*sin(omega)*cos(i)
P_ecl.y = sin(Omega)*cos(omega) + cos(Omega)*sin(omega)*cos(i)
P_ecl.z = sin(omega)*sin(i)

Q_ecl.x = -cos(Omega)*sin(omega) - sin(Omega)*cos(omega)*cos(i)
Q_ecl.y = -sin(Omega)*sin(omega) + cos(Omega)*cos(omega)*cos(i)
Q_ecl.z = cos(omega)*sin(i)
```

Map both vectors with `(x,y,z)_world = (x,z,-y)_ecl` and normalize them.

### 8.6 Orbit lines

Generate an ellipse from true anomaly samples using:

```text
r(nu) = a*(1 - e*e) / (1 + e*cos(nu))
```

Use the same P/Q basis as position propagation at the line's rebuild epoch. A cached orbit-line basis is a snapshot only; it must never cause the moving body's per-frame position to bypass current SEC/PER corrections.

Use enough samples to make high-eccentricity comet paths and close camera views smooth. Adaptive sampling earns more credit than one low fixed count.

## 9. Rate composition and corrections

Implementing only baseline Kepler motion is acceptable for an early milestone, but full credit requires the data-driven correction pipeline below.

### 9.1 Embedded physical rates

Planet records may contain nested blocks:

- `secular`: classical rates.
- `gr`: relativistic periapsis rate.
- `lt`: Lense-Thirring node and periapsis rates.

Normalize these to explicit degree-per-Julian-century components. If enabled/present:

```text
Omega_dot_total = Omega_dot_classical + Omega_dot_LT + Omega_dot_J2
i_dot_total     = i_dot_classical
omega_dot_total = omega_dot_classical + omega_dot_GR + omega_dot_LT + omega_dot_J2
```

At `T = simDaysTT / 36525`:

```text
Omega = Omega0 + T*Omega_dot_total
i     = i0     + T*i_dot_total
omega = omega0 + T*omega_dot_total
```

Do not add an angular rate twice merely because both a nested source field and a normalized total exist.

### 9.2 J2

`datasource.json.j2` contains the solar central-body parameters and, in the current snapshot, precomputed per-body node/periapsis rates. Prefer finite precomputed values. Respect global and per-body enable flags.

An implementation may compute a missing J2 rate from the central body's `J2`, equatorial radius, mean motion, eccentricity, and inclination, but it must test the units and document its convention.

### 9.3 Extra secular correction table (SEC)

Read `corrections.secular_terms` only when the root and target entry are enabled. Entries are matched to bodies by case-insensitive trimmed name.

Rates are degrees per Julian century. An entry can provide `Omega_dot`, `i_dot`, `omega_dot`, `varpi_dot`, `lambda_dot`, `M_dot`, and `phase_bias_deg`.

Segments:

- `start` is inclusive; `stop` is exclusive.
- Segment rates override only the fields they contain and inherit all other base rates.
- Sort segments by start date.
- Outside the listed range, clamp to the nearest first or last segment rather than dropping the correction.
- Date selection may use UTC midnight; the sub-day TT difference is irrelevant at this segment scale.

Apply SEC on top of the base physical-rate angles:

```text
Omega += T*Omega_dot
i     += T*i_dot
omega += T*omega_dot
```

Derive its mean-anomaly offset as follows:

```text
if lambda_dot or varpi_dot exists:
    v = varpi_dot if finite else Omega_dot + omega_dot
    l = lambda_dot if finite else Omega_dot + omega_dot + (M_dot or 0)
    dM = T*(l - v)
else if M_dot exists:
    dM = T*M_dot
else:
    dM = T*(Omega_dot + omega_dot)

dM += phase_bias_deg
```

Clamp eccentricity to `[0, 0.999999999]` and inclination to `[0, 180]` if a future correction path changes them.

### 9.4 Periodic correction table (PER)

Read enabled entries from `corrections.periodic_terms`. Each target term is:

```text
amplitude_deg * sin((frequency_deg_per_day * simDaysTT + phase_deg) in radians)
```

Important: ignore lambda terms whose label matches `equation of center` with spaces or underscores, case-insensitively. The elliptic Kepler solve already supplies the classical equation of center; adding it again double-counts the effect.

For the remaining enabled terms:

```text
dLambda = sum(lambda terms)
dVarpi  = sum(varpi terms)
omega  += dVarpi
dM     += dLambda - dVarpi
```

Preserve the upstream SEC `dM`; PER adds to it.

### 9.5 Optional Encke path

The supplied `corrections.encke_kick` configuration is experimental and currently disabled globally and for every target. A correct baseline should therefore use analytic propagation. Implementing the configured fixed-step perturbation path is optional bonus work only. It must be gated by both global and target flags and fall back safely to the analytic path.

## 10. Rotation and attitude

### 10.1 Physical pole

When `pole_RA_deg` and `pole_Dec_deg` exist, treat them as fixed ICRF/J2000 pole coordinates. The supplied pole-rate fields may be displayed but are not required to be propagated.

Convert the pole to equatorial Cartesian coordinates:

```text
x_eq = cos(dec)*cos(ra)
y_eq = cos(dec)*sin(ra)
z_eq = sin(dec)
```

Convert equatorial to J2000 ecliptic using mean obliquity:

```text
epsilon = 23.439291111 degrees
x_ecl = x_eq
y_ecl = y_eq*cos(epsilon) + z_eq*sin(epsilon)
z_ecl = -y_eq*sin(epsilon) + z_eq*cos(epsilon)
```

Then use the standard signed world mapping. Align the body's local `+Y` axis to this world pole with a quaternion. If pole coordinates are absent, `axial_tilt_deg` is an acceptable visual fallback.

### 10.2 Prime meridian and spin

All visual spin occurs around local `+Y`.

For non-Earth planets with finite IAU fields:

```text
W(days) = W0_deg + Wdot_deg_per_day*simDaysTT
spin angle = wrapTo2Pi(radians(W))
```

The sign of `Wdot_deg_per_day` is authoritative. This is essential for retrograde Venus and Uranus.

Fallback order when IAU fields are absent:

1. Signed `sidereal_day_hours`/`spin_direction`.
2. For a moon, signed orbital period.
3. A documented static or harmless visual fallback.

`spin_phase_deg` is a constant local texture seam offset applied once to the surface mesh. Do not add it in multiple hierarchy levels or fit it as a time-dependent correction.

### 10.3 Earth rotation

Earth must use Earth Rotation Angle, not the generic `W0 + Wdot*d` path:

```text
ut1Days = simDaysTT - 69.184/86400
ERA = 2*pi * (0.7790572732640 + 1.00273781191135448*ut1Days)
```

Wrap only for rendering. Do not add Equation of Time or Earth's orbital anomaly to Earth spin; solar-lighting changes already arise from Earth-Sun geometry. The supplied standard Earth map places Greenwich at the intended center and needs zero additional fitted offset.

### 10.4 Moons and tidal lock

Treat a moon as tidally locked when explicitly configured, or when:

```text
abs(spinPeriodDays - orbitPeriodDays) / orbitPeriodDays < 0.001
```

A locked moon must keep the same face toward its host after arbitrary forward/reverse animation and absolute date jumps. Derive its orientation geometrically from the current host direction; do not rely on accumulated spin.

Non-locked moons should use absolute spin from `simDaysTT`.

### 10.5 Rings

Create an annulus whose local normal is `+Y`, then attach it under the host's tilt node but outside the spin node. This makes the ring equatorial without spinning its texture unnecessarily.

Use the supplied alpha texture, double-sided transparency, and suitable depth handling. Respect `ring_texture_mode`; `strip` means the texture's radial coordinate should run from inner to outer radius. If explicit ring radii are unavailable, choose and document visually reasonable multiples of the host's display radius.

## 11. Sky, constellations, and deep-sky data

### 11.1 Star catalog

Each star record can include:

```text
hip
name
vmag
bv
ecl_lon_deg
ecl_lat_deg
```

Place a star on a large sphere centered on the camera using ecliptic longitude `lambda`, latitude `beta`, and radius `R`:

```text
x_ecl = R*cos(beta)*cos(lambda)
y_ecl = R*cos(beta)*sin(lambda)
z_ecl = R*sin(beta)
```

Then apply the standard ecliptic-to-world mapping. Brighter stars should appear larger/brighter than faint stars. Use `bv` to estimate color when finite. Render the catalog efficiently with buffer geometry/points and avoid one mesh per star.

Keep the sky centered on the camera so translation does not create parallax at Solar System scale. Do not let the sky write depth over foreground bodies.

On mobile or resource-constrained devices, loading only `skybox_star.json` is acceptable. Desktop full credit requires merging the ultra-faint `named_stars` array.

### 11.2 Constellations

`constellations.json` contains:

- `constellations`: 12 zodiac groups keyed by abbreviation.
- `constellations_other`: 76 other groups.
- `constellations_i18n`: localized display names.
- `constellations_images`: artwork plus image-space anchor points tied to HIP star IDs.

Each constellation value is an array of polylines, and each polyline is an array of HIP IDs. Resolve HIP IDs against the loaded star catalog and draw only valid adjacent pairs. A missing HIP must break or skip that segment safely; it must not connect unrelated stars across the sky.

Provide controls to toggle individual constellation lines, zodiac/all-other groups, and artwork independently. Artwork earns full credit when aligned to the spherical sky using its three or more image anchors rather than displayed as a flat screen overlay.

### 11.3 Deep-sky/nebula layer

Deep-sky entries are in `skybox_star.json.nebulae.entries`. Important fields include:

- `id`, `image`, and `world_ecl_deg`.
- Four `uv` corners.
- `catalog.name`, `catalog.otype`, magnitudes, size, distance, and cross IDs.
- Credits and optional source URL.

Use the four ecliptic sky corners and UVs to place each supplied transparent image as a sky patch. Batch, lazy-load, or level-of-detail this layer; eagerly uploading hundreds of full textures can exhaust mobile GPU memory.

Provide visibility, brightness/opacity, and pin/search controls for bonus credit. Object information must preserve available image credit.

## 12. Telescope mode

Telescope mode is an advanced requirement and a major differentiator between implementations.

Use `cities.json` to choose an observer latitude, longitude, and IANA timezone. Attach the conceptual observer to the rotating Earth, then orient the sky using the selected location and current approximate UT1.

A strong implementation provides:

- Country/region and city selectors generated from the data.
- Manual latitude/longitude entry.
- Altitude/azimuth readouts.
- Adjustable field of view.
- Alt-az and equatorial-style mount behavior, or a clearly documented subset.
- Optional horizontal/vertical mirroring and 180-degree rotation.
- Tracking of a selected star or deep-sky object.
- Correct exit behavior restoring the normal Solar System camera and UI.

Accuracy must be described honestly because the model does not include full precession-nutation, polar motion, refraction, or live EOP.

## 13. Information, diagnostics, and validation

### 13.1 Information panels

Display only fields that exist and clearly label units. Useful body fields include type, primary, physical radius, semi-major axis, eccentricity, inclination, orbital period, rotation period, pole, and data source. Do not display JavaScript `undefined`, `null`, or `NaN` as if they were measurements.

For stars and deep-sky objects, expose catalog names/IDs, magnitude, spectral color proxy, object type, angular size, distance, and credits where available.

### 13.2 Runtime correction controls

For full credit, expose toggles or diagnostics for:

- SEC extra secular terms.
- PER short-period terms.
- GR, LT, and J2 components.
- Light-time observed-position markers.
- Validation reference markers.
- AU/ecliptic grid.
- Phase lighting.

Changing a correction that affects geometry must update both body positions and orbit lines.

### 13.3 Light-time marker

An optional observed-position marker can be computed by fixed-point iteration:

```text
t_emit = t_observe - tau
tau_new = distance(body(t_emit), observer(t_observe)) / c
```

Use `c = 299792.458 km/s`, the same world scale as the scene, a bounded iteration count, and a convergence tolerance. The marker must use the same SEC/PER-aware propagation path as the visual body.

### 13.4 Validation sidecar

`data/validate.json.validate[bodyName]` contains rows with:

```text
year
x_AU
y_AU
z_AU
```

These reference coordinates are heliocentric ECLIPTIC/J2000, before the render-frame axis mapping. Samples represent the start of the named year for the project's approximate diagnostic comparison. Coverage differs by body; never claim a single date range for all planets.

A useful diagnostic should:

1. Choose a body and available year range.
2. Evaluate the implementation at the corresponding TT epoch.
3. Convert the simulated world position back to ecliptic AU, or map the reference to world consistently.
4. Report vector error and/or angular error.
5. Record which SEC/PER/GR/LT/J2 options were active.

The current data is empirical/model-oriented and does not establish one universal tolerance. Report results; do not hide failures or claim that unit tests prove astronomical accuracy.

## 14. Performance and engineering requirements

- Target smooth interaction on a normal desktop at 60 FPS and usable mobile behavior near 30 FPS.
- Avoid allocating vectors, matrices, arrays, and materials inside high-frequency animation loops.
- Reuse scratch objects and typed buffers.
- Use one draw call or a small bounded number for star magnitude/color groups.
- Cache textures by URL and configure color space correctly: color maps in sRGB; normal/data maps in a non-color space.
- Bound device pixel ratio on high-density displays.
- Dispose geometries, materials, textures, event listeners, timers, and controls when rebuilding or removing features.
- Do not use unbounded concurrency for hundreds of nebula textures.
- Handle rejected fetches and texture failures explicitly.
- Avoid global mutable state unless its ownership and lifecycle are clear.
- Keep orbital math testable without WebGL or DOM initialization.
- Keep data normalization separate from rendering.
- Make production output free of console floods and per-frame logging.

## 15. Required automated tests

At minimum, include tests for:

1. Primary datasource parses and contains a `bodies` array.
2. Body names used as primaries resolve to the Sun or another body.
3. Every used texture hint either exists or is reported by an asset audit.
4. Ecliptic-to-world conversion has the correct sign and remains right-handed.
5. P/Q basis vectors are finite, unit length, and mutually orthogonal.
6. `solveE` residual and continuity across circular, moderate, Halley, and near-one eccentricities.
7. Propagation of all 58 supplied records over representative negative and positive times produces no non-finite values.
8. High-eccentricity motion remains on the same continuous root branch.
9. Absolute body rotation is deterministic after a time jump.
10. Negative `Wdot` preserves retrograde spin.
11. Earth ERA matches the stated formula at J2000 and at another epoch.
12. SEC segment boundaries are inclusive/exclusive as specified and clamp out of range.
13. PER filters classical equation-of-center labels and preserves upstream `dM`.
14. Optional sidecar failure does not invalidate the primary Solar System model.

Tests should run from one documented command and must not require a browser for pure mathematical/data cases. Add browser smoke tests if the chosen toolchain makes them practical.

## 16. Progressive milestones

An Agent should keep the app runnable at the end of each milestone.

### Milestone A: foundation

- Project scaffold, development server, production build, and tests.
- Loading/error UI.
- Renderer, camera, controls, and responsive shell.
- Validated data normalization.

### Milestone B: correct Solar System

- Sun and all valid bodies.
- Safeguarded Kepler solver.
- Correct signed coordinate mapping.
- Parent-relative moon systems.
- Orbit paths and absolute simulation clock.

### Milestone C: attitude and visual quality

- Data-driven textures, pole alignment, absolute spin, Earth ERA, rings, atmospheres, and tidal lock.
- Selection, focus, labels, information panel, and polished responsive controls.
- Lighting modes, halo, and comet presentation.

### Milestone D: correction model

- Embedded secular/GR/LT/J2 rate composition.
- SEC segments and mean-anomaly policy.
- PER filtering and composition.
- Geometry rebuilds and correction diagnostics.

### Milestone E: sky and observation

- Efficient full star catalog.
- Constellation lines and artwork.
- Deep-sky imagery and pinning.
- Telescope mode using city data.
- Reference-data diagnostics.

## 17. Evaluation rubric (100 points)

### A. Mathematical and astronomical correctness: 35

- 8: Correct J2000/TT time model and deterministic absolute-time behavior.
- 8: Robust continuous elliptic solver, including Halley and `e = 0.999999999`.
- 7: Correct right-handed ecliptic-to-world mapping and P/Q basis.
- 6: Correct parent-relative moon propagation and orbit-line agreement.
- 6: Correct poles, signed spins, Earth ERA, texture phase, and tidal lock.

### B. Data-driven completeness: 20

- 6: All valid Sun/body records created without a parallel hard-coded catalog.
- 5: Texture, ring, atmosphere, and frame fields handled robustly.
- 5: Physical rates plus SEC/PER/J2 composition implemented correctly.
- 4: Optional sidecars and missing assets degrade gracefully.

### C. Rendering and user experience: 20

- 5: Attractive, coherent, legible 3D presentation.
- 5: Selection, focus, time, date, speed, labels, halo, and orbit controls.
- 4: Responsive desktop/mobile interaction and accessible UI basics.
- 3: Effective lighting, Earth maps, rings, atmosphere, comet, and shadows.
- 3: Smooth performance and stable camera behavior at extreme scales.

### D. Sky and advanced features: 15

- 4: Efficient base plus ultra-faint star rendering.
- 3: Constellation lines, localization, and anchored artwork.
- 3: Deep-sky image layer with useful controls and credits.
- 3: Telescope mode based on city/observer data.
- 2: Validation, light-time, tours, recording, or other well-executed diagnostics.

### E. Engineering quality: 10

- 3: Clear modular design and maintainable naming without unnecessary abstraction.
- 3: Meaningful automated tests covering numerical edge cases.
- 2: Deterministic install/build/serve documentation and clean production output.
- 2: Resource lifecycle, error handling, bounded work, and no obvious per-frame allocation problems.

### Automatic major deductions

- Mirrored/left-handed world caused by omitting the signed axis conversion: up to -15.
- Halley moves backward, jumps branches, freezes, or becomes non-finite: up to -15.
- Date jumps produce different state depending on how the date was reached: up to -10.
- Retrograde planets spin in the wrong direction: up to -8.
- Bodies or orbital elements are manually duplicated instead of read from data: up to -10.
- Application cannot boot without a private service or secret: result is not reviewable.

## 18. Acceptance checklist

A reviewer should be able to answer yes to all core items:

- [ ] A clean checkout containing the Agent's work, `data/`, and `images/` installs and runs from documented commands.
- [ ] Production build succeeds without modifying supplied data/assets.
- [ ] The app boots through HTTP and shows a recoverable error for a failed primary fetch.
- [ ] Sun, 8 planets, 5 dwarf planets, 37 moons, and 8 comets are represented when all supplied records validate.
- [ ] Planet, dwarf, moon, and comet orbit visibility can be controlled independently.
- [ ] Halley remains finite and moves continuously in forward and reverse time.
- [ ] Earth, Venus, and Uranus rotate in their intended signed directions/models.
- [ ] A repeated jump to the same date yields the same positions and orientations.
- [ ] Rings are equatorial to their host poles.
- [ ] The base star catalog renders efficiently and uses catalog coordinates.
- [ ] Selecting and focusing a moving body remains stable.
- [ ] Pure math/data tests pass from one command.
- [ ] The application visibly displays `Copyright Terry Wan` in a reasonably discoverable location.
- [ ] The implementation is original even if the public demo was used as a behavioral or visual reference.
- [ ] The Agent documents implemented milestones, deliberate omissions, and remaining scientific limitations honestly.

## 19. Scientific limitations that must remain visible

Even an excellent implementation must disclose:

- Orbital time is TT with no separate TDB propagation.
- Earth uses a fixed approximate TT-UT1 value and no live EOP.
- Pole RA/Dec rates need not be propagated; fixed J2000 poles are acceptable here.
- The production solver is elliptic only.
- SEC/PER values are supplied model adjustments, not a universal accuracy guarantee.
- Validation coverage varies by body and ends at different years.
- Encke perturbation is experimental and disabled in the supplied configuration.
- Lighting and atmosphere are visualization aids, not radiometric models.
- Display radii may be exaggerated relative to orbital distances.

## 20. Final instruction to the implementing Agent

First make the mathematics testable, then make the scene correct, then make it beautiful. Prefer a smaller working milestone over a broad collection of broken controls, but continue through as many milestones as time permits.

Do not merely draw spheres on circles. The supplied data is rich enough to demonstrate robust high-eccentricity motion, three-dimensional orbital planes, physical pole orientation, signed rotation, sky catalogs, constellations, deep-sky imagery, observer geometry, and empirical diagnostics. Use it.

When finished, report:

1. What was implemented.
2. Which milestone was reached.
3. How to install, test, build, and run it.
4. Test results and known failures.
5. Performance strategy.
6. Scientific limitations and any assumptions made.
