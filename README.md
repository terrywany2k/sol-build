# Solar System Agent Build Challenge 🌌

How much of a complete 3D Solar System can an AI coding Agent build from a detailed specification, raw astronomical data, and image assets alone?

This public challenge invites you to give an Agent only:

```text
Build.md
data/
images/
```

The Agent must create the application from scratch. It receives no original HTML, CSS, JavaScript, tests, package configuration, screenshots, or hidden implementation details.

## 🎯 Purpose

This is a practical test of an Agent's ability to:

- Understand a large technical specification.
- Design and complete a real browser application independently.
- Implement robust orbital mathematics instead of drawing planets on simple circles.
- Interpret unfamiliar JSON schemas and use supplied assets correctly.
- Balance scientific correctness, visual quality, performance, testing, and user experience.

Different Agents may choose completely different architectures and designs. The challenge measures the quality and completeness of the result, not whether it reproduces an existing codebase.

## 🪐 The challenge

The supplied data includes the Sun, planets, dwarf planets, moons, comets, orbital corrections, rotation models, stars, all 88 IAU constellations, deep-sky objects, observing locations, and validation samples.

A strong result may include:

- Continuous elliptic Kepler propagation, including Halley's Comet.
- Correct three-dimensional orbital planes and signed coordinate conversion.
- Planetary poles, prograde/retrograde rotation, Earth Rotation Angle, rings, atmospheres, and tidal locking.
- Interactive time controls, date jumps, selection, camera focus, labels, and diagnostics.
- Catalog-based stars, constellation lines and artwork, nebula imagery, and Telescope mode.
- Automated numerical tests and a reproducible production build.

The complete requirements, algorithms, milestones, acceptance checklist, and 100-point evaluation rubric are in [Build.md](./Build.md).

## ✨ Reference demo

An existing demonstration of the intended product experience is available here:

[https://solar-a7l.pages.dev/](https://solar-a7l.pages.dev/)

Participants may use the public page as a visual and behavioral reference. The challenge implementation must still be original: do not copy, download, recover, or reverse-engineer the demo's source code.

## 🚀 How to participate

1. Fork or download this challenge repository.
2. Give your chosen Agent the repository, with `Build.md`, `data/`, and `images/` as its only starting materials.
3. Ask it to implement as much of [Build.md](./Build.md) as possible.
4. Keep the Agent's source code, tests, build instructions, and final report.
5. Score the result using the rubric in `Build.md` and share what worked, what failed, the Agent/model used, and how much human assistance was provided.

For a fair comparison, disclose any extra prompts, manual edits, external files, or intervention given after the initial task.

## 📋 Minimum submission information

Please include:

- Agent and model name/version.
- Prompts and important follow-up instructions.
- Level of human intervention.
- Implemented milestone and rubric score.
- Install, test, build, and run commands.
- Screenshots or a deployed demo.
- Known failures and scientific limitations.

## 💫 Attribution

All completed applications must visibly retain:

```text
Copyright Terry Wan
```

Participants may add separate implementation credits, but must not imply ownership of Terry Wan's supplied data, images, project concept, or original work.

### 🖼️ Third-party image notice

Some image and texture assets included with this challenge were collected from publicly available internet sources, including Solar System Scope, NASA, and other astronomy projects, institutions, and individual creators. Copyright and other rights in those third-party materials remain with their respective owners. Their inclusion in this challenge does not transfer ownership to Terry Wan or to challenge participants.

NASA material is not automatically assumed to cover every asset in this repository, and the mention of NASA or Solar System Scope does not imply their endorsement of this project. Before redistributing the assets separately or using them commercially, participants are responsible for identifying the original source and confirming the applicable copyright, licence, attribution, and trademark requirements.

Several small-moon textures are AI-generated placeholders rather than scientifically accurate source imagery: Metis, Adrastea, Atlas, Janus, Epimetheus, Proteus, and Nereid. They should be replaced with appropriately licensed and source-attributed imagery when suitable assets are available.

Have fun, compare approaches, and see how far your Agent can go. 🚀
