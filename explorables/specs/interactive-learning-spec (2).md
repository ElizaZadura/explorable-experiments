Here is the specification for the interactive essay.

**Title:** Taming the Machine: The Architecture of Agent Harnesses
**Concept:** An explorable explanation of how we moved from simple prompts to complex "Harnesses" to solve the problems of Context Rot and Compounding Errors in AI agents.
**Tech Stack:** Single-file HTML, CSS (Inter font, clean academic aesthetic), Vanilla JS.

---

### **Layout Overview**
A central column of scrolling narrative text (max-width 650px). Interactive visualizations break out into full-width "figures" embedded directly between paragraphs. The aesthetic should be "Modern Textbook"—lots of whitespace, distinct typography for code/variables, and subtle animations.

---

### **Section 1: The Problem of "Vibe Coding"**

*   **Narrative:** Start by explaining that early AI coding was just "prompt and pray" (Vibe Coding). Introduce the constraint: **Bounded Attention**. LLMs have a fixed context window. As a conversation gets long, the model "forgets" the beginning or gets "lost in the middle."
*   **Visual (The Context Bucket):**
    *   A visual representation of a Context Window (a bar or container).
    *   A stream of "Tokens" (colored blocks) entering the container.
*   **Interaction:**
    *   A button labeled **"Add Code Feature"**.
    *   Clicking it adds a block of tokens to the context window.
    *   **The Logic:** Once the container hits a limit (e.g., 8 blocks), the *oldest* blocks turn red and fade out ("Context Rot").
    *   **Dynamic Label:** A text display showing: `Current Context: [#############] (Memory Full - Forgetting Initial Instructions)`.
*   **Pedagogical Goal:** Visually demonstrate why a single long chat session fails for complex software projects.

### **Section 2: The Harness Architecture**

*   **Narrative:** Introduce the solution: The **Agent Harness**. Explain that instead of one long chat, we break the process into specialized agents and distinct sessions, connected by *persistent state* (files/artifacts).
*   **Visual (The System Diagram):**
    *   A schematic based on the video's "Anthropic/LangChain" architecture.
    *   **Left:** `Initializer Agent`
    *   **Center:** `State / Artifacts` (represented as a file icon `feature_list.json` and `progress.txt`).
    *   **Right:** `Task Agent` (Loop).
*   **Interaction (The Simulation):**
    *   A "Play" control to step through the lifecycle.
    *   **Step 1:** Initializer reads `spec.txt` -> Animation shows it writing to the central `feature_list.json` icon.
    *   **Step 2:** Task Agent wakes up -> Reads `feature_list.json` -> Writes code -> Updates `progress.txt` -> Dies (Context Cleared).
    *   **Step 3:** Task Agent wakes up *again* (fresh context) -> Reads `progress.txt` to know where it left off.
*   **Deep Dive Toggle:** A switch labeled "Show Data Structure". When on, display the raw JSON of the `feature_list` updating in real-time as the user steps through the simulation.
*   **Pedagogical Goal:** Show that the "Brain" isn't the LLM anymore; the "Brain" is the *State File* that persists between agent sessions.

### **Section 3: The Mathematics of Reliability**

*   **Narrative:** Address the second unsolved problem: **Reliability**. Explain that even a 95% accurate agent fails miserably over long tasks due to compounding errors.
*   **The Equation:** Render the formula clearly:
    $$P_{success} = (P_{step})^{N}$$
    Where $P_{step}$ is the accuracy of a single step, and $N$ is the number of steps.
*   **Interaction:**
    *   Two sliders embedded directly in the text:
        1.  `Agent Accuracy` (90% to 99.9%)
        2.  `Number of Steps` (1 to 100)
*   **Visual:** A dynamic line graph showing the probability of success dropping as steps increase.
*   **Guided Discovery:**
    *   Text prompt: "Set the Agent Accuracy to 95% (which sounds good). Now set Steps to 20 (a typical coding task)."
    *   **Dynamic Output:** Large bold text calculation: **"Total System Reliability: 35.8%"**.
    *   Text prompt: "Notice how quickly it becomes unusable? This is why 'Vibe Coding' fails for large apps."

### **Section 4: The Solution - Human-in-the-Loop & Checkpoints**

*   **Narrative:** Explain that since we can't easily get LLMs to 99.99% accuracy yet, the Harness must implement **Checkpoints** and **Human-in-the-loop** (HITL). This resets the error probability curve.
*   **Visual:** The same graph from Section 3.
*   **Interaction:**
    *   Add a toggle: **"Enable Human Checkpoints"**.
    *   **Visual Logic:** When enabled, the graph curve "resets" to 100% every 5 steps (simulating a human reviewing the code and fixing errors).
    *   **Dynamic Output:** Update the Total Reliability calculation. It should jump from ~35% back up to ~95% (assuming the human catches the errors).
*   **Conclusion Text:** "The Harness doesn't make the AI smarter; it creates a safety net that allows us to trust the output of a probabilistic machine."

---

### **Technical Implementation Notes**

*   **CSS:** Use CSS Grid for the Architecture diagram to ensure responsive layout. Use SVG for the connecting lines between agents and state files so they scale cleanly.
*   **State Management:** Use a simple JS object to track the "Simulation State" (Current Step, Files Content, Context Load).
*   **Math:** Use a simple JS function to calculate $R = r^n$ and update the DOM elements `innerText` immediately on slider `input` events. Do not use a heavy charting library; build a simple SVG line chart or CSS bar chart for lightweight performance.

The app must be fully responsive and function properly on both desktop and mobile. Provide the code as a single, self-contained HTML document. All styles and scripts must be inline. In the result, encase the code between "```" and "```" for easy parsing.