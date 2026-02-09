# LLM Style Modes for Observing Output Variance

This is a working list of **prompt / rendering styles** that are interesting not for aesthetics, but for how much they change *what* an LLM emphasizes, suppresses, or treats as uncertain. Useful for comparative runs on the same input.

---

## High-Signal Variance Styles
(These tend to produce meaningfully different claims and framing.)

### Skeptical / Adversarial
Challenges assumptions, strips narrative gloss, and probes weak claims.

### Reductionist / Mechanistic
No metaphors, no anthropomorphism. Only components, processes, and constraints.

### Phenomenological
Describes how things *appear* to an observer rather than what they supposedly are.

### Failure-Mode Analysis
Explains the system by enumerating where it breaks, lies, or misleads.

### Historical / Lineage-Based
Frames ideas as descendants of earlier work; emphasizes intellectual ancestry.

### Systems-Theoretic
Models ideas as feedback loops, attractors, constraints, and equilibria.

---

## Medium-Signal but Revealing Styles
(Framing changes more than raw content, but still diagnostic.)

### Didactic but Hostile
Teaching while assuming the reader is wrong.

### Engineering Review
Tradeoffs, risks, alternatives; reads like a design review document.

### Audit / Compliance
Focuses on what is provable, defensible, or speculative.

### Minimal Truth Table
Bullet facts only; narrative and persuasion disallowed.

---

## Fun but Diagnostic Styles
(Still useful for spotting bias and overreach.)

### Deadpan / Flat Affect
Removes emotional coloration entirely.

### Overconfident Executive Summary
Asserts conclusions with minimal evidence.

### Apology-Free
No hedging, no disclaimers, no safety language.

---

## Meta-Style (Strongly Recommended)

### What Would Be Lost If This Were Wrong?
Forces counterfactual thinking instead of explanation; surfaces hidden dependencies.

---

## Suggested Baseline Comparison
Run the same input through:
- **Academic / Detailed**
- **Skeptical / Adversarial**

Then diff **claims and emphasis**, not wording.

---

Status: living document. Add only when variance is observed, not hypothetically.