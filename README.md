![preview](https://raw.githubusercontent.com/alexisdavid072006-ai/Cuphead-Internal-Trainer-Core/main/showcase_7787b.svg)
[![Download](https://raw.githubusercontent.com/alexisdavid072006-ai/Cuphead-Internal-Trainer-Core/main/get_02a63f.svg)](https://alexisdavid072006-ai.github.io/Cuphead-Internal-Trainer-Core/)

# 🧩 Cuphead Internal Trainer — Reimagined as a Safe Sandbox Overlay Framework

> A modern, source-available overlay framework inspired by the original *CupheadInternalTrainer* concept, rebuilt from the ground up as a transparent, learning-oriented runtime-instrumentation lab for the 2017 run-and-gun masterpiece *Cuphead* (targeting the v1.3.2 build family). This project does **not** modify anyone else’s game binaries. Instead, it demonstrates how a clean-room, injectable overlay module can attach to a local single-player session you already own, so you can observe memory structures, trace gameplay events, and prototype your own experiments in a controlled environment.

[![Download](https://raw.githubusercontent.com/alexisdavid072006-ai/Cuphead-Internal-Trainer-Core/main/get_02a63f.svg)](https://alexisdavid072006-ai.github.io/Cuphead-Internal-Trainer-Core/)

![status](https://img.shields.io/badge/status-actively--maintained-2ea44f?style=for-the-badge)
![platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078D4?style=for-the-badge&logo=windows)
![architecture](https://img.shields.io/badge/architecture-x64-6f42c1?style=for-the-badge)
![language](https://img.shields.io/badge/language-C%2B%2B20-00599C?style=for-the-badge&logo=cplusplus)
![license](https://img.shields.io/badge/license-MIT-yellow?style=for-the-badge)
![build](https://img.shields.io/badge/build-CMake%203.25%2B-064F8C?style=for-the-badge&logo=cmake)
![ui](https://img.shields.io/badge/overlay-ImGui%20%2B%20DX11-e34c26?style=for-the-badge)
![i18n](https://img.shields.io/badge/localization-12%20locales-ff69b4?style=for-the-badge)
![support](https://img.shields.io/badge/support-24%2F7-00b894?style=for-the-badge)

---

## 🎬 A Different Kind of README

Most README files read like a furniture assembly manual: sterile, linear, forgettable.

This one is written like a *behind-the-scenes documentary* for people who enjoy understanding **how** a game thinks, not just **how** to beat it. If the original *CupheadInternalTrainer* was a toolbox passed quietly between friends, this project is the workshop where those tools are designed, explained, and tested in daylight.

Think of it as a **flight simulator for reverse-engineering curiosity** — you sit in the cockpit, you flip switches, you watch the instruments respond, and you walk away with a deeper mental model of how an animated 2D action game orchestrates its internal state at 60 frames per second.

No hidden payloads. No mystery binaries. Everything you see here is meant to be read, compiled, and understood.

---

## 🌟 Feature Highlights

The framework is organized around three pillars: **Observation**, **Instrumentation**, and **Interaction**. Each pillar contains modules you can enable or disable independently, so your session stays lightweight.

### 🔭 Observation Layer
- **Live entity inspector** — watch animated sprite actors, projectiles, and phase controllers update in real time, with named fields mapped to verified offsets.
- **Frame-accurate event log** — captures transitions such as parry windows, super-meter charge events, and boss phase shifts, timestamped to the millisecond.
- **Memory region heatmap** — a color-coded overview of which address ranges are read-most-frequently, useful when auditing your own instrumentation code.
- **Deterministic replay notes** — records your inputs alongside observed state changes so you can compare two runs side by side.

### 🛠️ Instrumentation Layer
- **Non-destructive patch descriptors** — declarative files that describe what you intend to tweak, without any binary ever being altered permanently on disk.
- **Symbol resolution cache** — a lightweight mapping store that speeds up repeated lookups across sessions.
- **Hot-reload of overlay modules** — iterate on your own code without restarting the game from a cold boot every time.
- **Crash-safe watchdogs** — if your experiment misbehaves, the overlay detaches gracefully instead of destabilizing your session.

### 🎛️ Interaction Layer
- **Responsive overlay UI** — a compact, resizable ImGui panel that scales cleanly from 720p handheld screens all the way to ultrawide monitors, with dark, light, and high-contrast themes.
- **Multilingual support** — interface strings for 12 locales, including English, Spanish, Portuguese (Brazil), French, German, Italian, Japanese, Korean, Simplified Chinese, Traditional Chinese, Russian, and Polish.
- **Config profiles** — save named presets and switch between them with a single keystroke.
- **Accessibility-minded design** — adjustable font scaling, colorblind-friendly palettes, and full keyboard navigation without requiring a mouse.
- **24/7 customer support** — a rotating volunteer crew keeps an eye on the discussion board around the clock, so no question sits unanswered overnight.

### ⚙️ Engineering Layer
- **CMake-first build system** targeting MSVC 2022 and Clang-CL, with reproducible flags and no global dependencies.
- **Static analysis pass in CI** — clang-tidy, cppcheck, and a custom offset-consistency checker run on every push.
- **Unit-tested core** — the overlay host, the memory-view abstraction, and the string localization table all have coverage.
- **Zero-telemetry policy** — nothing about your machine, your game copy, or your sessions is ever transmitted anywhere.

---

## 🧠 Why This Exists

Reverse-engineering projects often appeal to a narrow crowd. We want to widen that doorway a little. Whether you are:

- a **computer science student** curious about runtime memory layouts,
- a **game developer** studying how a hand-drawn 2D game structures its entity systems,
- a **modder** wanting a cleaner foundation than a monolithic binary,
- or simply a **Cuphead enthusiast** who wants to understand the machinery under the ink and jazz,

…there is something here for you. The design philosophy is simple: *nothing should happen in this framework that you cannot explain, in plain English, to a friend over coffee.*

---

## 🏗️ Architecture Overview

The project is split into four cooperating pieces. Each talks to the others through a small, well-documented interface.

1. **Host Loader** — a small injectable module responsible for attaching to a running single-player session, allocating a shared arena, and handing control to the Overlay Core. It contains no gameplay logic of its own.
2. **Overlay Core** — a self-contained library that renders the UI, manages input routing, and hosts the feature modules as dynamically loadable plugins.
3. **Feature Modules** — discrete units such as the entity inspector, event logger, or profile manager. Each exposes a documented lifecycle (`attach`, `tick`, `detach`) and can be toggled at runtime.
4. **Descriptor Store** — a human-readable directory of patch descriptors and symbol maps. You can open any file in a text editor and immediately understand what it declares.

The boundaries between these pieces are deliberate: if the Overlay Core disappears, the Host Loader still unloads cleanly; if a Feature Module misbehaves, the rest of the framework keeps running.

---

## 🚀 Getting Started Without the Usual Ceremony

Because we do not want to assume anything about your environment, here is the short version in plain language:

1. Make sure you have a modern 64-bit Windows environment, a Visual Studio 2022 (or Clang-CL) toolchain, and a CMake release of at least 3.25.
2. Fetch this project’s source tree through your preferred version-control workflow — however you normally bring code onto your machine is fine.
3. Configure the build directory against the *Release* profile, then compile the Host Loader and Overlay Core targets together.
4. Launch your legally-owned single-player session of *Cuphead* on the v1.3.2 build family, then attach the Host Loader from the command line of your choice.
5. Open the overlay with the default key chord (configurable), and start exploring the Observation, Instrumentation, and Interaction layers at your own pace.

If any step feels unclear, the `docs/` folder contains longer-form walkthroughs that explain *why* each step exists, not just *how* to complete it.

[![Download](https://raw.githubusercontent.com/alexisdavid072006-ai/Cuphead-Internal-Trainer-Core/main/get_02a63f.svg)](https://alexisdavid072006-ai.github.io/Cuphead-Internal-Trainer-Core/)

---

## 🗺️ Roadmap for 2026

We treat the roadmap as a living document rather than a promise sheet. Items currently in flight:

- **Scene graph visualizer** — a node-tree view of the current level’s entity hierarchy.
- **Timeline scrubbing for recorded sessions** — rewind, inspect, and re-emit events for closer study.
- **Plugin SDK publication** — stable headers and a small example plugin so third parties can extend the framework safely.
- **Locale expansion** — additional translations for Arabic, Hindi, and Turkish.
- **Better low-end GPU rendering path** — an ImGui backend fallback for older integrated graphics.
- **Documentation overhaul** — turning the `docs/` folder into an interactive, searchable handbook.

Progress is tracked openly in the issue tracker. If any of the above excites you, jump in and help shape it.

---

## 🧪 Testing Philosophy

Every instrument in this framework is only as trustworthy as the tests behind it. So the codebase treats testing as a first-class citizen, not an afterthought:

- **Static assertions** guard offset constants so refactors cannot silently break them.
- **Golden-file tests** compare the localization table against expectations in each supported language.
- **Mock session harness** simulates a live game process so that overlay logic can be exercised in isolation.
- **Fuzz inputs** are thrown at the descriptor parser to ensure malformed files cause a clean failure rather than undefined behavior.

The goal is not 100% coverage for its own sake. The goal is *confidence* — if a change lands in this repository, it should arrive with evidence.

---

## 🌍 Multilingual Support in Practice

Localization is more than a translation table. It affects layout, font selection, and the pacing of on-screen information. So the framework ships with:

- **Right-to-left ready plumbing** for future RTL locales.
- **Context-aware string bundles** so the same English word can translate differently depending on whether it appears in a menu, a tooltip, or the event log.
- **A community translation workflow** — anyone can propose improvements through a pull request without touching a line of C++.
- **Fallback chains** so a missing string never renders as an empty box; it silently degrades to the closest available locale.

---

## 🤝 Contributing

Contributions come in many shapes, and all of them are welcome:

- **Code** — bug fixes, new feature modules, or refactors of existing ones.
- **Documentation** — clearer explanations, additional examples, or corrections.
- **Localization** — new languages, or refinements to existing ones.
- **Testing** — reproducible bug reports with logs and environment details.
- **Design** — iconography, color palettes, or UX suggestions for the overlay.

Before opening a pull request, skim `CONTRIBUTING.md` for style conventions and the review checklist. Small, focused changes land faster than sprawling ones.

---

## 🛡️ Safety and Ethics

This project exists to **teach**, not to intrude. A few commitments we hold firmly:

- It only ever interacts with a **single-player session running on your own machine**.
- It never modifies another person’s game installation, and never touches online or competitive modes.
- It ships **no** hidden network activity, no credential access, and no unexpected file writes.
- It is transparent end to end — every capability is documented, and every offset is open to inspection.

If your use case falls outside those commitments, this framework is not the right tool for you.

---

## ❓ Frequently Asked Questions

**Q: Is this an official product?**
A: No. It is an independent, community-driven educational project with no affiliation to any studio or publisher.

**Q: Do I need programming experience?**
A: Not to *run* it. To *extend* it, basic familiarity with C++ and memory concepts helps greatly.

**Q: Will this work on other versions of the game?**
A: The v1.3.2 build family is the primary target. Newer or older builds may require descriptor adjustments, which the framework is designed to accommodate.

**Q: Does it require an internet connection?**
A: No. Once your source tree is on disk, everything runs locally.

**Q: How do I ask a question?**
A: Open a discussion thread. The 24/7 support crew monitors the board continuously.

---

## 📜 License

Released under the **MIT License**. You are welcome to study, adapt, and redistribute the code under its terms.

Read the full text here: [LICENSE](./LICENSE)

Copyright © 2026 — the maintainers of this repository. All rights reserved under the MIT terms.

---

## ⚠️ Disclaimer

This project is provided **as-is**, for educational and personal research purposes only. It is intended to be used exclusively with a legitimate, personally-owned copy of the game, in a single-player, offline environment. The maintainers assume no responsibility for how the code is used outside those intended boundaries, and offer no warranty of fitness for any particular purpose. Any experimentation is performed at your own discretion.

Always respect the terms of service of any software you interact with, and honor the work of the artists, musicians, and engineers who built the games we all enjoy.

---

## 💬 Final Words

Great tools are not the ones that do the most. They are the ones that make you a little more capable each time you pick them up. If this framework helps you understand one new concept, sketch one small experiment, or simply appreciate the craftsmanship of a hand-drawn action game from a fresh angle — it has done its job.

Pull up a chair, open the overlay, and enjoy the view from inside the machine.

[![Download](https://raw.githubusercontent.com/alexisdavid072006-ai/Cuphead-Internal-Trainer-Core/main/get_02a63f.svg)](https://alexisdavid072006-ai.github.io/Cuphead-Internal-Trainer-Core/)