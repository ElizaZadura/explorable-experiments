# Index Page Redesign

**Date:** 2026-04-16  
**Status:** Approved — ready for implementation

---

## Goal

Redesign `index.html` to scale comfortably to 80+ explorables. The current flat list of ~20 items already feels unwieldy; publishing the full unpublished collection would make it unusable. The new design groups explorables by topic, makes style variants (game / academic / skeptical) visible without cluttering, and lets visitors narrow the list by category or keyword.

---

## Approach

**Hybrid: topic sections + sticky filter bar** (chosen over flat-list-with-tags and pure card-grid).

- Topic sections provide editorial structure for browsing
- A sticky filter bar (search input + category chips) lets visitors narrow quickly when they know what they want
- Falls back gracefully without JS — sections are still readable as plain HTML
- Stays a single static `index.html` file, no build step or server required

---

## Visual Design

| Property | Value |
|---|---|
| Background | `#1d1d1f` |
| Surface (input, chips) | `#2d2d2f` |
| Body text | `#f5f5f7` |
| Muted text | `#86868b` |
| Link / accent | `#6e6ef5` |
| Border | `#424245` |
| Section marker colour | `#6366f1` (indigo, uniform across all sections) |
| Max content width | `800px` |
| Border radius | `3–4px` (rectangular, not pill-shaped) |

Section headings use a **left border accent** (3px solid indigo) — same indigo for all sections, no per-category colour variation. Headings are small-caps uppercase in muted text.

---

## Structure

### Header
Title ("Explorable Experiments") and one-line description, same copy as current.

### Sticky filter bar
Two rows, stuck to top of viewport on scroll:
1. **Search input** — filters visible entries by title keyword (JS, client-side)
2. **Category chips** — one chip per section: All · AI & ML · Agents & Systems · Physics & Science · Security · Quantum & Computation · Git · AI Economics · Case Studies. Clicking a chip hides all other sections. "All" resets. Active chip styled with indigo tint.

### Topic sections (8)
Each section has:
- A `section-heading` with the left-border indigo accent
- A list of `entry` rows separated by `1px solid #424245` borders

### Entry rows
Each entry contains:
- **Title link** — links to the primary / default file for that topic
- **Description** — one line, muted colour
- **Variant pills** (optional) — only shown when a topic has multiple style versions. Each pill links directly to that variant file. Rectangular (`border-radius: 3px`), colour-coded by style:

| Style | Background | Text | Border |
|---|---|---|---|
| game | `#052e16` | `#4ade80` | `#166534` |
| academic | `#0c1a3d` | `#93c5fd` | `#1e3a6e` |
| skeptical | `#2d1200` | `#fb923c` | `#7c2d12` |
| beginner | `#1e0a2e` | `#c084fc` | `#6b21a8` |

---

## Categories and Members

### AI & Machine Learning
Core ML concepts — how models work, training, parameters.

- Neural Network Playground
- The Trillion Sliders
- The Mechanics of Pre-Training `academic`
- How to Train Your AI `game` `academic`
- Inside the Black Box
- How Computers See Numbers `beginner`
- The Learning Illusion `skeptical`

### AI Agents & Systems
Agent architectures, memory, orchestration, harnesses.

- The Anatomy of an AI Agent
- Agent Architecture Sandbox
- Agentic Patterns `academic` `game`
- The Architecture of Agentic Systems `academic` `game`
- Taming the Machine (agent harnesses)
- The Context Bottleneck
- The Agent Expert
- The Ceiling of Automation
- The Ralph Loop `game` `skeptical`
- Escaping the Context Window
- The Age of Agents `skeptical`

### Physics & Everyday Science
Mechanics, geometry, everyday phenomena.

- The Geometry of Packing
- The Topology of the Fitted Sheet `skeptical`
- Stress, Shear & Survival
- The Mechanics of Magic
- The Algorithm of Salsa
- The Geometry of the Cascade
- The Algorithm of Sparkle
- The Immune System — An Interactive Battle
- The Unstable Equilibrium `skeptical`
- Diamond Painting Academy `game`

### Security & Red Teaming
Locks, AI safety, adversarial attacks, jailbreaking.

- Security by Imperfection
- The Mechanics of Security
- The Psychology of AI Red Teaming
- Adversarial Alignment `academic` `game` `skeptical`
- The Art of the Jailbreak `game`
- The Fragility of Alignment `skeptical`

### Quantum & Computation
Quantum mechanics, linear algebra, computation theory, mind.

- The Quantum Observer Effect
- The Linear Race
- The Fraught Road to Quantum Advantage `academic` `skeptical` `game`
- The Limits of Computation
- The Non-Computable Mind
- More Than a Machine `beginner`

### Git & Version Control
Git internals as interactive explainers.

- Git: The Time Traveler's File System
- The Directed Acyclic Graph — An Anatomy of Git
- Git: The Immutable Graph

### AI Economics & Limits
Hype, profit, critical takes on where AI actually is.

- The AI Profit Paradox
- Betting Against AI
- The Evolving Limits of AI `skeptical`
- The AI Skill Ceiling `skeptical` `game`
- The Age of Agents / Thread-Based Engineering `skeptical`
- The Thread-Based Engineering Manifesto `skeptical`
- The Entropy of Agentic Threads `skeptical`
- The Truth Filter

### Case Studies
Post-mortems, real-world analysis, incident audits.

- The "No-Code" Catastrophe (Moltbook)
- Autopsy: The Moltbook Incident `skeptical`
- The Architecture of a Crash Out `game`
- Case Study: The Fitted Sheet Manifold `skeptical`
- Case Study: The Recursive Illusion `skeptical`
- Autopsy: The Moltbook Incident (full version)

---

## JavaScript Behaviour

All JS is vanilla, inline in `index.html` — no dependencies.

**Search:** `input` event on the search field. For each `.entry`, check if `entry-title` text contains the query (case-insensitive). Hide non-matching entries. If all entries in a section are hidden, hide the section heading too.

**Category filter:** Click on a `.cat-chip` sets it active and shows only the matching `.section`, hiding all others. Clicking "All" resets. Search and category filter compose — search runs within the currently visible section(s).

**No-JS fallback:** All sections and entries are visible by default. The filter bar is still rendered but inert.

---

## Files Changed

- `index.html` — full rewrite of styles and content structure
- `.gitignore` — add `.superpowers/` entry if not present

---

## Out of Scope

- Pagination or separate category pages
- Server-side rendering or build tooling
- Adding new explorable content (separate step after index is live)
- Moving / renaming files in `explorables/unpublished/`
