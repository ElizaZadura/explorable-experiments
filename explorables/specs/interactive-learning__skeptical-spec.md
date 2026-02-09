Here is the design specification for the interactive essay.

# SPECIFICATION: The AI Skill Ceiling

**Theme:** Skeptical / Adversarial / Engineering Reality Check
**Tone:** Socratic, Direct, slightly "Cyberpunk/Terminal" aesthetic.
**Core Argument:** AI is a probabilistic tool applied to a deterministic domain. Without "Hard Skills" (understanding the deterministic machine), you are bound by the AI's probabilistic error rate, leading to a "Complexity Collapse."

---

## Layout & Aesthetic
- **Visual Style:** Dark mode, Monospace fonts (Courier, Fira Code), high contrast (neon green/amber on black). Looks like a developer's markdown documentation or a terminal log.
- **Structure:** Single-column vertical scroll. Text blocks are short, punchy, and interspersed with interactive diagrams.
- **Responsiveness:** Canvas elements resize to container width. Controls are touch-friendly.

---

## Section 1: The "Hello World" Trap
**Goal:** Acknowledge AI's capability on small tasks, then immediately challenge its scalability.

*   **Text:** "So, you've heard the advice: *'Don't learn to code. The AI will do it for you.'* It sounds liberating. For simple tasks, it feels like magic. But is it engineering?"
*   **Interaction:** A button labeled **[ Generate Script ]**.
*   **Visual:** A small box representing a "Project."
*   **Logic:**
    *   Clicking the button instantly fills the box with green "Code" blocks.
    *   Status label: "Success. Time: 0.1s."
*   **The Turn (Text):** "That was easy. But real engineering isn't about starting projects. It's about *maintaining* them as they grow."

## Section 2: The Mechanism (Probabilistic vs. Deterministic)
**Goal:** Explain *why* AI fails at complexity. It predicts text, it doesn't "know" logic.

*   **Text:** "Here is the fundamental friction. Computers are **Deterministic** (Logic). LLMs are **Probabilistic** (Statistics)."
*   **The Math:** Display the simplified LLM function:
    $$P(w_i | w_{1}...w_{i-1})$$
    *(The probability of the next word given the previous words).*
*   **Interaction:** A "Next Token" visualizer.
    *   Input field: "The function `calculateTax` should return..."
    *   Visual: A bar chart showing the top 3 predicted next tokens with percentages (e.g., `Integer (80%)`, `String (15%)`, `Null (5%)`).
*   **Control:** A slider for **Temperature** (Randomness).
*   **Guided Discovery:**
    *   *Instruction:* "Slide the Temperature to 0. Notice the output is rigid. Slide to 1.0. Notice the output creates syntax errors."
    *   *Lesson:* "To be creative, AI risks being wrong. To be safe, AI risks being useless. You, the human, must judge the difference."

## Section 3: The "Sloshing" Effect (The Core Simulation)
**Goal:** Visualize The Primeagen's concept of bugs "sloshing back and forth" when the user lacks the skill to steer the AI.

*   **Text:** "The Primeagen argues: As complexity grows, an AI-reliant developer enters the 'Sloshing Phase.' You fix one bug, but because you don't understand the system, you introduce two more."
*   **Simulation:** A dynamic line graph plotting **Codebase Size** vs. **Stability**.
*   **Controls:**
    1.  **Complexity Slider:** (Low = Todo List, High = Enterprise Cloud Architecture).
    2.  **Hard Skills Slider:** (Low = "I just prompt", High = "I know the stack").
    3.  **Action Button:** **[ Fix Bug ]**
*   **Visual Logic:**
    *   The graph draws in real-time.
    *   If **Hard Skills** < **Complexity**: Clicking "Fix Bug" might lower the current bug count, but increases "Technical Debt" (hidden variable).
    *   Eventually, the graph becomes volatile (oscillating wildly) — this is the "Sloshing."
*   **The "Under the Hood" Toggle:**
    *   Shows the formula: `NewBugs = (Complexity / Skill) * Random(0.5, 1.5)`.
    *   *Message:* "When Complexity exceeds Skill, you are no longer the pilot. You are the passenger."

## Section 4: The "Intern" Factor (Taste & Context)
**Goal:** Address the "Taste" argument. AI satisfies the prompt, not the architecture.

*   **Text:** "AI is like an intern who doesn't care. It wants to finish the ticket. It doesn't care if the code is unmaintainable next year."
*   **Visual:** Two diagrams of a system architecture.
    *   **Left (The Prompted Solution):** A messy web of dependencies (Spaghetti code).
    *   **Right (The Engineered Solution):** Clean, modular boxes.
*   **Interaction:** Hover over a "Change Request" button (e.g., "Switch Database").
*   **Visual Feedback:**
    *   On the Spaghetti diagram, 80% of the nodes light up red (Breaking Changes).
    *   On the Engineered diagram, only 1 node lights up red.
*   **Socratic Conclusion:** "If you can't distinguish between these two diagrams, you are building a trap for your future self."

## Section 5: Conclusion
**Goal:** Synthesis.

*   **Text:** "AI is a thruster. Hard Skills are the steering wheel. If you have a massive thruster and no steering wheel, you don't go faster. You crash harder."
*   **Final Call to Action:** A toggle switch: "Rely on AI" vs "Master the Machine."
    *   *Rely on AI:* Text fades to: "Good luck with the sloshing."
    *   *Master the Machine:* Text fades to: "Welcome to the real work."

---

## Technical Constraints Checklist
*   [x] **Single HTML File:** All CSS/JS embedded.
*   [x] **No External Libraries:** Vanilla JS for the graph (using HTML5 Canvas).
*   [x] **Responsive:** CSS Grid/Flexbox for layout.
*   [x] **Math Rendering:** Use simple HTML/CSS for formulas (no heavy MathJax).

The app must be fully responsive and function properly on both desktop and mobile. Provide the code as a single, self-contained HTML document. All styles and scripts must be inline. In the result, encase the code between "```" and "```" for easy parsing.