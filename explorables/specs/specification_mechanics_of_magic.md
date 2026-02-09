Here is the specification for the **Interactive Essay: The Mechanics of Magic (The Slip Force)**.

This design treats the card trick not as a puzzle, but as a study in physics, friction, and visual perception.

***

# Title: The Mechanics of Magic: The Slip Force
**Layout:** Vertical Scrolling "Scrollytelling" Article
**Theme:** Dark mode (Magician's table aesthetic), clean typography (San Francisco/Inter), distinct "Simulation" containers.

---

### Section 1: The Spectator's Perspective (The Hook)
**Goal:** Establish the illusion before explaining it. The user acts as the spectator.

*   **Text:** "Magic relies on the gap between what you see and what actually happens. In the 'Slip Force,' the goal is to make a spectator think they have cut to a random card, while actually forcing the top card of the deck upon them."
*   **Visual:** A top-down view of a deck of cards on a black table (CSS rendered). The top card is visually distinct (e.g., Jack of Diamonds), but face down.
*   **Interaction:** 
    *   A button labeled **"Riffle"**. Clicking it animates the cards riffling down the side (CSS animation).
    *   A button labeled **"Stop"**. 
*   **Logic:** No matter when the user clicks "Stop," the animation splits the deck. The top packet is removed. The card "cut to" is revealed.
*   **The Reveal:** Text appears: "You stopped at a random location. But look closer. The card you 'cut' to is the **Jack of Diamonds**—the card that was on top of the deck the entire time. How?"

---

### Section 2: X-Ray Vision (The Mechanism)
**Goal:** Expose the mechanical reality of the move using a "God View."

*   **Text:** "To understand the Slip Force, we must look at the deck from the side. The secret lies in the fingers of the hand holding the deck."
*   **Visual:** A **Side-Profile View** (Cross-section) of the deck. 
    *   The "Force Card" (Top Card) is highlighted in **Red**.
    *   The rest of the cards are white.
    *   Ghostly outlines of fingers are shown gripping the deck.
*   **Interaction:** A horizontal slider labeled **"Time Scale"** (0% to 100% of the move).
*   **Simulation Logic:** 
    *   As the user drags the slider, the deck splits at a random point.
    *   **Crucial Detail:** As the top packet moves to the right (simulating the hand pulling it away), the **Red Force Card** does *not* move with the top packet. It slides off and lands on the bottom packet.
*   **Guided Discovery:** Text updates as you scrub: "Drag slowly. Notice that while the top packet moves right, the top card stays stationary, falling onto the bottom packet."

---

### Section 3: The Physics of Friction (The Theory)
**Goal:** Explain *why* the card stays behind. It's not magic; it's friction coefficients.

*   **Text:** "Why does the top card stay behind? It's a battle of friction. The friction between your fingers and the card ($F_{finger}$) must be greater than the friction between the cards ($F_{cards}$)."
*   **The Equation:** Render the inequality centered on screen:
    $$F_{finger} > F_{cards}$$
*   **Visual:** The same Side-Profile view, but simplified to just the Top Packet and the Force Card. Force vectors (arrows) appear on the card.
*   **Interaction:** Two Range Sliders embedded in the text.
    1.  **"Finger Pressure"** (Controls gripping force).
    2.  **"Deck Condition"** (Controls card slickness/stickiness).
*   **Logic:**
    *   **Scenario A (Success):** High Pressure, Slick Cards. The arrow for $F_{finger}$ is huge. The card stays put. Text: "Success. The fingers pin the card in place while the packet slides out."
    *   **Scenario B (Fail):** Low Pressure. The arrow for $F_{finger}$ shrinks. The card moves *with* the top packet. Text: "Fail. You didn't apply enough pressure. The card was pulled away with the packet."
    *   **Scenario C (Fail):** Sticky Cards (Old deck). The arrow for $F_{cards}$ grows. The card drags along. Text: "Fail. The cards are clumping together."

---

### Section 4: The Speed of Perception (The Execution)
**Goal:** Teach that speed hides the mechanism.

*   **Text:** "The mechanism is obvious in slow motion. To sell the illusion, the 'Slip' must happen faster than the eye can track."
*   **Visual:** The Top-Down view from Section 1 again.
*   **Interaction:** A slider labeled **"Performance Speed"** (Slow Motion -> Real Time).
*   **Challenge:** A button "Perform the Cut".
*   **Logic:**
    *   **Slow Speed:** The user clearly sees the top card sliding off. Feedback: "Too slow. The spectator saw the slide."
    *   **Fast Speed:** The animation is so fast (CSS `transition-duration: 0.1s`) that it looks like a clean cut. The slide is imperceptible (motion blur effect).
*   **Conclusion Text:** "By combining the correct finger pressure with a swift motion, the mechanics of the slip vanish, leaving only the illusion of a free choice."

---

### Technical Implementation Notes for the Engineer:
1.  **CSS Cards:** Use `div` elements with absolute positioning for the cards. For the side view, use thin rectangles (`height: 2px`).
2.  **Animation:** Use CSS Transforms (`translateX`, `translateY`) controlled by JavaScript variables based on the sliders.
3.  **Responsiveness:** The card deck visualization must scale down for mobile screens.
4.  **Single File:** All CSS and JS must be embedded in `<style>` and `<script>` tags within the HTML.

The app must be fully responsive and function properly on both desktop and mobile. Provide the code as a single, self-contained HTML document. All styles and scripts must be inline. In the result, encase the code between "```" and "```" for easy parsing.