Here is the design specification for a single-file, gamified Interactive Essay based on the video content.

# Specification: "The Architect of Agents"
**Subtitle:** A Gamified Guide to AI Workflow Design Patterns

## 1. Global Design & Tone
*   **Visual Style:** "Clean Cyberpunk." Dark mode background (`#0f172a`), neon accent colors (Cyan for logic, Pink for errors, Green for success), rounded glass-morphism cards, and monospace fonts for data streams.
*   **Gamification Elements:**
    *   **Progress Bar:** A "System Integrity" bar at the top that fills as the user completes modules.
    *   **The "Run" Button:** Every simulation requires the user to hit a satisfying, pulsing "Execute" button.
    *   **Tone:** The user is addressed as "Architect." The text is instructional but framed as a briefing.

## 2. Narrative Structure & Sections

### Module 0: The Agent Definition (Hook)
*   **Concept:** AI Agents = LLM + Tools + Planning.
*   **Text:** "Welcome, Architect. Standard LLMs just talk. **Agents** do work. An Agent is a system where the LLM's output controls the workflow."
*   **Interactive Simulation:** "The Hello World of Agency"
    *   **Visual:** A simple chat input and a "Terminal" window.
    *   **Task:** Ask the AI to "Check the server status."
    *   **Mechanism:**
        1.  User types request.
        2.  **Visual Logic:** Show the LLM output *not* as text to the user, but as a JSON command: `{ "tool": "check_status", "args": "server_01" }`.
        3.  The "Terminal" executes the code.
        4.  The LLM interprets the result.
    *   **Teaching Point:** Show that the LLM isn't answering the user directly; it's talking to a function first.

---

### Module 1: The Chain (Prompt Chaining)
*   **Concept:** Breaking a task into fixed, sequential subtasks.
*   **Context from Video:** The "Investment Advisor" example.
*   **Text:** "Level 1: Linear Logic. We need to build an Investment Bot. If we ask it to do everything at once, it hallucinates. We must chain the thoughts."
*   **Interactive Simulation:** "Chain Reactor"
    *   **Visual:** A horizontal pipeline with three nodes: `Idea Generator` -> `Niche Breakdown` -> `Decision Gate`.
    *   **Controls:** The user can toggle the "Gate" on or off.
    *   **Input:** User selects a topic (e.g., "Tech Stocks").
    *   **Animation:**
        1.  **Node 1:** Generates a high-level idea.
        2.  **Node 2:** Drills down into a niche (e.g., "Semiconductors").
        3.  **Node 3 (The Gate):**
            *   *If Gate is OFF:* The agent blindly recommends investing (Risk: High).
            *   *If Gate is ON:* The agent acts as a classifier (as per video). It checks the budget. If budget < threshold, it halts.
    *   **Code Expose:** Show the prompt passing from one node to the next. `Output 1` becomes `Input 2`.

---

### Module 2: The Router (Routing)
*   **Concept:** Directing an input to a specialized agent.
*   **Context from Video:** Customer Service / Data Analytics vs. RAG.
*   **Text:** "Level 2: Traffic Control. Generalist models are slow. We need specialists. Your goal: Route the query to the correct expert."
*   **Interactive Simulation:** "The Switchboard"
    *   **Visual:** An input stream at the top, a central "Router Brain," and three destination buckets at the bottom:
        1.  *General Chat*
        2.  *Refund Specialist*
        3.  *Data Analyst (Python Tool)*
    *   **Challenge:** Incoming queries fall from the top (e.g., "Plot this CSV," "I want my money back," "Tell me a joke").
    *   **Control:** The user must tweak the **Router System Prompt** by selecting keywords (e.g., "Select 'plot', 'graph' for Data Analyst").
    *   **Feedback:** If the user sends a "Plot" request to the "Refund Specialist," the agent errors out. When routed correctly, the Data Analyst shows a mini-graph.

---

### Module 3: Parallelization (The Coordinator)
*   **Concept:** Breaking a massive task into concurrent chunks.
*   **Context from Video:** Summarizing a large document/legal contract.
*   **Text:** "Level 3: Speed. We have a 100-page contract. Reading it linearly takes too long. We need a **Coordinator**."
*   **Interactive Simulation:** "The Hive Mind"
    *   **Visual:** A large document icon representing "The Contract."
    *   **Controls:** A slider for `Shard Count` (1 to 5 workers).
    *   **Mechanism:**
        *   *Slider at 1:* A single progress bar moves slowly across the document. Result: Slow.
        *   *Slider at 5:* The document splits into 5 chunks. 5 small progress bars fill simultaneously (fast).
        *   **Aggregator:** Once all 5 finish, a final block merges them into a summary.
    *   **Math/Logic Display:** Show the trade-off.
        *   `Time Taken = Total_Tokens / N_Workers`
        *   `Cost = Total_Tokens * Cost_Per_Worker` (Show that cost remains roughly the same, but speed increases).

---

### Module 4: Evaluator-Optimizer (The Loop)
*   **Concept:** The "Most Important" pattern. Generating, checking, and refining.
*   **Context from Video:** Robustness and self-correction.
*   **Text:** "Final Level: Self-Correction. Agents make mistakes. An **Evaluator-Optimizer** loop forces the agent to fix its own work before showing you."
*   **Interactive Simulation:** "The Code Forge"
    *   **Goal:** The Agent must write a specific Python function (simulated).
    *   **Visual:** A loop cycle: `Generator` -> `Output` -> `Evaluator` -> `Feedback` -> `Generator`.
    *   **Controls:**
        *   *Loop Limit:* How many times can it retry?
        *   *Strictness:* How high must the score be to pass?
    *   **Action:**
        1.  User hits "Generate".
        2.  **Attempt 1:** Agent produces code.
        3.  **Evaluator:** (Simulated) "Error: Syntax Invalid." (Red Flash).
        4.  **Feedback:** The error is fed back into the Generator.
        5.  **Attempt 2:** Agent fixes syntax. Evaluator: "Logic Error."
        6.  **Attempt 3:** Agent fixes logic. Evaluator: "Accepted." (Green Flash).
    *   **Takeaway:** Show that without the loop, the user would have received the broken Attempt 1.

## 3. Technical Implementation Strategy

*   **File Structure:** `index.html` containing:
    *   `<style>` block for Tailwind-like utility classes and animations.
    *   `<body>` with distinct `<section>` tags for each module.
    *   `<script>` block using Vanilla JS (ES6+).
*   **State Management:** A simple `gameState` object to track unlocked levels and simulation variables.
*   **Responsiveness:** Use CSS Grid `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))` for the simulation dashboards so they stack on mobile.
*   **No External Assets:** All icons will be SVG strings within the HTML. All logic is client-side simulation (no actual API calls to OpenAI/Anthropic to keep it free and fast, but mimicking the latency and logic of real calls).

## 4. Example Code Snippet (Style of the "Router" Logic)

```javascript
// The Logic the user interacts with in Module 2
const routerSimulation = (userQuery, keywords) => {
    // VISUALIZE: Highlight the "Router" node
    highlightNode('router-brain');
    
    // THE MECHANISM: Simple keyword matching acting as a classifier
    let destination = 'general_chat';
    
    if (keywords.data.some(k => userQuery.includes(k))) {
        destination = 'data_analyst';
    } else if (keywords.refund.some(k => userQuery.includes(k))) {
        destination = 'refund_specialist';
    }
    
    // EXPOSE THE LOGIC: Update the UI text to show the decision
    document.getElementById('router-log').innerText = 
        `Input: "${userQuery}"\nDetected Intent: ${destination.toUpperCase()}\nRouting...`;
        
    // ANIMATE: Send packet to the correct bucket
    animatePacketTo(destination);
}
```

## 5. Success Criteria
The user succeeds if they can reach the bottom of the page having "configured" all 4 patterns correctly. The final screen displays a "Senior Architect Certification" badge rendered in HTML/CSS.

The app must be fully responsive and function properly on both desktop and mobile. Provide the code as a single, self-contained HTML document. All styles and scripts must be inline. In the result, encase the code between "```" and "```" for easy parsing.