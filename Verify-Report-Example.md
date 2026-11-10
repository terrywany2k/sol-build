# Verification report example

Use this structure to write `VERIFY.md` for the selected edition. Replace the
illustrative fields and rows with observed results from the submitted public
deployment. List every mandatory check from the selected brief, and link larger
tables or machine-readable evidence when the edition requires them. The example
entries below are fictional and demonstrate format only.

## Release

| Field | Example |
| --- | --- |
| Edition | Advance |
| Public application URL | `https://observatory.example/` |
| Release ID and test date | `<deployed version or build ID>`, `<UTC date>` |
| Public access check | `<browser and observed result when opening the URL signed out>` |
| Desktop environment | `<browser/version, OS, viewport>` |
| Mobile environment | `<browser/version, device or touch emulation, viewport>` |

## Models, coverage, and sources

Summarize the physical scale, orbit and observer models where applicable, and
supported dates. Identify the source, frame, units, time conventions, and asset
licenses needed to reproduce the checks. List coverage and accuracy limits
separately.

## Acceptance results

| Requirement | Setup and steps | Expected result | Observed result and evidence | Status |
| --- | --- | --- | --- | --- |
| Advance date coverage | Jump to the first supported instant, a date near the middle, and the last supported instant. Return to the starting instant on the public build | Required planets and moons evaluate at all three dates and the original state is repeatable | Example only. Record the tested instants, the results for the required bodies, and a capture or numeric comparison | Not run |
| Advance observer directions | Set a site and UTC instant and compare a planet and the Moon against an independent reference under matched conventions | Report both altitude and azimuth differences | Example only. Provide site, instant, reference and its convention, app values, and differences in degrees | Not run |
| Mobile walkthrough | Select a target, use the camera, change time, and inspect the observing result | Controls are reachable and the workflow completes | Example only. Record the tested device or emulation, observed behavior, and any friction | Not run |

Use **Pass** for an observed result that meets the requirement, **Fail** for an
observed mismatch, **Blocked** for a check prevented by a specific dependency,
and **Not run** for an untested check. Record the reason for any failure,
blocker, or untested check. Mark the overall result **Fail** if a mandatory
requirement fails, **Incomplete** if mandatory checks remain blocked or untested,
or **Pass** once every mandatory requirement has passing evidence.

## UI/UX and optional features

Summarize the observed first-use workflows and any interaction friction on the
tested screens. For each optional feature claimed, give its user value, how to
try it on the public build, and the evidence that it works.

| Scoring area | Self-assessment | Evidence or reason |
| --- | --- | --- |
| Core requirements | `<score>/100` | `<checks and deductions>` |
| UI/UX quality | `<score>/30` | `<observed interactions and deductions>` |
| Additional features | `<score>/20` | `<feature scores and evidence>` |
| Total | `<sum>/150` | `<mandatory gates still open, if any>` |

## Gaps and handoff

List open failures, untested environments, model limits, and any gap between the
tested release and the public URL. Finish with the public link and the overall
acceptance status so the reviewer can reproduce the result.
