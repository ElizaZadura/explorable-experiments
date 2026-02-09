Here is the design specification for **"The Geometry of Packing: Rolling vs. Folding"**, an interactive explorable explanation based on the provided video.

### **Title:** The Geometry of Packing: Rolling vs. Folding
**Concept:** An interactive essay investigating the physics of volume, the geometry of bin packing, and the efficiency of motion in the context of packing a suitcase.
**Tech Stack:** Single-file HTML5, Vanilla JavaScript, CSS Grid/Flexbox, SVG for visualizations.

---

### **Global Layout Strategy**
*   **The Scroll:** The user scrolls through a central narrative column (max-width: 650px).
*   **The Stage:** Interactive figures are embedded directly within the text flow (not a sidebar).
*   **Typography:** High-readability serif font (e.g., Georgia or Merriweather) for text; Monospace for data/math; Sans-serif for UI controls.
*   **Color Palette:** Clean, academic aesthetic. Off-white background, dark grey text, muted pastels for clothes (Sage Green, Slate Blue, Clay Red) to match the video's aesthetic.

---

### **Section 1: The Intuition vs. Reality**
**Goal:** Challenge the user's preconception about space saving.

*   **Text:** "When packing for a trip, the eternal debate is Folding vs. Rolling. Intuition suggests that rolling clothes compresses them, saving massive amounts of space. But is that true?"
*   **Interactive Element: The Prediction Slider.**
    *   **Visual:** A graphic of an empty suitcase (top-down view).
    *   **Control:** A slider labeled "Guess the Space Saving of Rolling." (Range: 0% to 50%).
    *   **Action:** As the user slides, a text label updates: "I bet rolling saves [X]% more space than folding."
*   **The Reveal (Triggered on button click):**
    *   **Animation:** Two piles of clothes appear. One folds into the suitcase, one rolls. They fill the suitcase to the *exact same level*.
    *   **Data Overlay:** "Actual Difference: ~0%."
    *   **Text:** "Surprising? In our experiment, both methods consumed the exact same volume. A cotton fiber is a solid; you can't change its volume just by bending it differently. However, that doesn't mean the methods are equal."

### **Section 2: Conservation of Volume (The Physics)**
**Goal:** Explain *why* space is equal and introduce the variable that actually matters (Air/Compression).

*   **Text:** "A t-shirt is a deformable solid. Whether you fold it into a rectangle or roll it into a cylinder, the amount of fabric remains constant. The equation for volume is:"
*   **Interactive Element: The Shape Shifter.**
    *   **Visual:** A side-profile view of a single t-shirt.
    *   **The Equation:** Displayed prominently: $$Volume = Mass / Density$$
    *   **Controls:**
        1.  **Toggle Switch:** [Folded Mode] / [Rolled Mode].
        2.  **Slider:** "Compression Force" (representing the user squeezing the air out).
    *   **Simulation Logic:**
        *   *Folded Mode:* The shirt is a flat rectangle ($Height = h$).
        *   *Rolled Mode:* The shirt is a circle ($Area = \pi r^2$).
        *   **Key Interaction:** Toggling between Fold and Roll changes the *shape* but maintains the *area* visually.
        *   **Slider Interaction:** Increasing "Compression" shrinks the shape and updates the equation's denominator (Density).
    *   **Feedback Text:** "Notice: Changing the shape doesn't shrink the shirt. Only applying **Force** (removing air) reduces the volume."

### **Section 3: The Bin Packing Problem (The Geometry)**
**Goal:** Explain why rolling *feels* more efficient (fitting into gaps).

*   **Text:** "If volume is conserved, why do travelers prefer rolling? It solves the **Bin Packing Problem**. Suitcases aren't perfect rectangles—they have wheel wells and handle ridges. Large rigid shapes (folded clothes) waste space in corners."
*   **Interactive Element: The Tetris Simulation.**
    *   **Visual:** An irregular container (a suitcase cross-section with wheel bumps in the corners).
    *   **Task:** "Fit 6 items into the case."
    *   **Controls:** Two buttons: [Add Folded Stack] vs [Add Rolled Cylinders].
    *   **Simulation:**
        *   *Folded:* Drops large rectangular blocks. They bridge over the wheel wells, leaving empty white "void space" underneath.
        *   *Rolled:* Drops smaller circular units. They tumble into the corners and wheel wells.
    *   **Real-time Metric:** A "Void Space" percentage meter.
    *   **Lesson:** Rolling reduces *Void Space*, not *Item Volume*. It allows you to utilize the nooks and crannies.

### **Section 4: The Algorithm of Time (Efficiency)**
**Goal:** Visualize the time difference (11m vs 17m) shown in the video.

*   **Text:** "The most significant difference wasn't space, but **Time**. Rolling is a simpler algorithm to execute."
*   **Interactive Element: The Complexity Calculator.**
    *   **Visual:** Two animated hands performing the tasks side-by-side.
    *   **The Math:**
        *   $$Time_{Fold} = (AlignSeams + Flatten + Fold_1 + Fold_2 + Smooth) \times Items$$
        *   $$Time_{Roll} = (FoldHalf + RollFast) \times Items$$
    *   **Controls:**
        *   Slider: "Number of Items" (1 to 20).
        *   Slider: "Perfectionism" (Low to High).
    *   **Logic:**
        *   High perfectionism drastically increases $Time_{Fold}$ (because folding requires precision to sit flat).
        *   Rolling is resilient; even a messy roll is fast.
    *   **Output:** A dynamic bar chart comparing "Total Minutes" based on the user's inputs.
    *   **Video Reference:** "As seen in the video, Rolling (11:18) beat Folding (17:53) by over 6 minutes."

### **Section 5: The Exception (Structural Integrity)**
**Goal:** Address the "Collared Shirt" rule.

*   **Text:** "Algorithms have edge cases. The video notes one major exception: **The Collared Shirt**."
*   **Interactive Element: The Stress Map.**
    *   **Visual:** An SVG illustration of a dress shirt.
    *   **Interaction:** Hover over the shirt to see "Structural Zones."
        *   *Collar:* High rigidity requirement.
        *   *Sleeves:* Low rigidity requirement.
    *   **Toggle:** [Apply Roll Force].
    *   **Result:** When rolled, the collar turns red (Damage Warning). Text appears: "Rolling crushes rigid structures. For collared shirts, the flat fold is required to maintain structure."

### **Summary / Footer**
*   **Conclusion:** "The Verdict: Roll for speed and gap-filling. Fold for structure and organization. Space is (mostly) an illusion."
*   **Credits:** "Based on the experiment by The Folding Lady."

---

### **Technical Implementation Notes (For the Engineer)**

1.  **SVG Manipulation:** Use inline SVGs for the clothes. Use CSS `transform: scale()` for the compression slider. Use `d` path interpolation (or simple opacity switching) to morph between Folded (rect) and Rolled (circle) states.
2.  **Physics Engine (Lite):** For Section 3 (Bin Packing), use a very lightweight 2D physics library like `Matter.js` (embedded via CDN or minified in file) OR write a simple bounding-box logic if keeping it strictly zero-dependency. *Recommendation: Matter.js makes the "tumbling" into corners feel visceral and satisfying.*
3.  **Responsive Design:** The interactive containers should use `aspect-ratio` CSS property to maintain dimensions on mobile. The "Bin Packing" section might need to stack vertically on small screens.
4.  **State:** Use a single `const state = { compression: 0, items: 10, ... }` object and a `render()` loop to update the DOM elements based on state changes. This ensures the "Equation" text always matches the visual.

The app must be fully responsive and function properly on both desktop and mobile. Provide the code as a single, self-contained HTML document. All styles and scripts must be inline. In the result, encase the code between "```" and "```" for easy parsing.