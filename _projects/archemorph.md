# Building ArcheMorph: A Deep Dive into a Client-Side Personality Profiler

As developers, we often encounter projects that blend intriguing concepts with tangible technical challenges. ArcheMorph, a multifaceted personality profiling system, was one such endeavor. This post explores the technical architecture, key decisions, and the development journey of creating this entirely client-side application.

The goal of ArcheMorph is to provide users with a detailed, 4-part personality archetype and in-depth analysis of 16 psychological factors, all processed directly in their browser for privacy and immediate feedback.

## Core Technical Architecture: Purely Client-Side

From the outset, a key requirement was user privacy and a seamless experience without backend dependencies for the core quiz and result generation. This led to a purely client-side architecture using:

*   **HTML:** For structuring the landing page, quiz interface, results display, and informational content pages.
*   **CSS:** For styling all aspects of the user interface, including a responsive design for various screen sizes and a print-optimized stylesheet for saving results. We recently implemented a dark theme with black backgrounds, purple accents, and teal text, which presented its own set of UI/UX considerations, especially around contrast.
*   **JavaScript (Vanilla JS):** The powerhouse of the application. All logic resides here, including:
    *   Dynamic question loading.
    *   User response collection.
    *   Score calculation (including handling reversed items and sub-scores for the Motivational Style axis).
    *   Personality code generation.
    *   Complex archetype name generation based on score patterns across 16 traits.
    *   Dynamic display of results, including detailed blurbs for High/Moderate/Low trait scores and alternative archetype suggestions for moderate scores.
    *   Client-side routing (via simple page links) for informational pages.
*   **`data.js`:** A crucial decision was to centralize all static data – questions, archetype component names, trait definitions, naming rule maps, and blurbs – into a single JavaScript file. This makes maintenance and updates more manageable than embedding data directly within HTML or the main `script.js`.

## Key Technical Features & Implementation Details

### 1. Dynamic Quiz Generation

The quiz consists of 145 questions across 14 primary axes. Instead of hardcoding these in HTML, `script.js` dynamically generates the quiz interface:
*   It iterates through `PRIMARY_AXIS_CODES_FOR_QUESTIONS` (defined in `data.js`).
*   For each axis, it retrieves the corresponding questions from `QUESTIONS_BANK` (also in `data.js`).
*   HTML elements for each question and its 1-6 Likert scale radio buttons are created and appended to the DOM.
*   This approach keeps `quiz.html` clean and allows for easier modification of questions in `data.js`.

### 2. Score Calculation and Normalization

Upon submission:
*   User responses (1-6) are collected using `FormData`.
*   For each of the 16 scorable traits (including sub-axes M_H, M_G, M_R derived from the 'M' primary axis), scores are calculated:
    *   Reversed items are inverted (e.g., a '1' becomes a '6' on a 1-6 scale).
    *   The sum of scores for an axis is divided by the number of questions for that axis, resulting in a normalized score between 1 and 6.
*   The Motivational Style ('M') questions are processed specially, with each question contributing to one of three sub-scores (Head, Gut, Heart).

### 3. Archetype Name Generation: The Logic Core

This was one of the most complex parts, translating quantitative scores into qualitative archetype names.
*   **Trait Groupings:** The 16 scorable traits are divided into four logical groups, each influencing one part of the 4-part archetype name. This is defined in `TRAIT_GROUPINGS` in `data.js`.
*   **Binary Pattern Mapping:** For each group, the scores of its constituent traits are compared against `MID_LIKERT_POINT`. This creates a binary pattern (e.g., High-Low-High-Low becomes `true,false,true,false`).
*   **Lookup Maps:** Four extensive JavaScript objects (`CORE_PERSONALITY_MAP`, `SUFFIX_MODIFIER_MAP`, etc., in `data.js`) map these binary patterns directly to specific names (e.g., "Executive," "Conceptualizing"). These maps were ported from Python dictionaries.
    *   Group 1 (4 traits) -> 2<sup>4</sup> = 16 Core Personalities.
    *   Group 2 (3 traits) -> 2<sup>3</sup> = 8 Suffix Modifiers.
    *   Group 3 (4 traits) -> 2<sup>4</sup> = 16 Prefix Modifiers.
    *   Group 4 (5 traits) -> 2<sup>5</sup> = 32 Part 4 Qualifiers.
*   This deterministic mapping ensures consistency and allows for a vast number of unique archetype combinations (16 * 8 * 16 * 32 = 65,536).

### 4. Nuanced Results: Handling Moderation

To provide deeper insight beyond simple high/low scores:
*   We defined a `GRAY_AREA_DELTA` (e.g., +/- 0.75 around the midpoint). Scores falling within this range are considered "Moderate."
*   **`TRAIT_DESCRIPTIONS`:** A new data structure in `data.js` holds blurbs for "High," "Low," and "Moderate" interpretations for each of the 16 traits.
*   **Alternative Archetype Parts:** If a trait score is "Moderate," the system temporarily "flips" the score (just above/below midpoint) and re-runs the relevant archetype part determination function (e.g., `determineCorePersonality`). If this results in a *different* name part, it's presented to the user as a potential alternative expression of their personality, highlighting their flexibility. This logic is encapsulated in a `getAlternativeNamePartIfFlipped` helper function.

### 5. UI Enhancements & Static Content Delivery

Recently, the project expanded from a single quiz page to a small static site:
*   **Landing Page (`index.html`):** Introduces the system with clear calls to action. Uses CSS Flexbox for responsive info cards.
*   **Informational Pages (`archetypes.html`, `factors.html`):** These pages dynamically load and display content (blurbs, trait descriptions) from `data.js` using a separate `info-page-loader.js`. This keeps the information consistent with the quiz data without manual HTML updates.
*   **Navigation:** A consistent header navigation menu is present across all pages.
*   **Utility Features:**
    *   "Retake Quiz": `window.location.reload()`.
    *   "Save as PDF/Print": `window.print()` with a dedicated `print-style.css`.
    *   "Share Archetype": Uses `navigator.share` API with a fallback to `prompt()`.

## Challenges & Learnings

*   **Data Management:** Centralizing all question text, blurbs, and mapping rules into `data.js` was crucial for maintainability. Manually porting Python dictionaries to JS objects required careful attention to syntax.
*   **CSS Complexity:** Implementing the dark theme and ensuring good contrast with teal text on black backgrounds, plus styling all the dynamic content, required careful CSS organization. The "last row centering" for the info card grid was best solved using Flexbox's `justify-content: center`.
*   **Client-Side Logic:** Writing extensive logic (score calculation, name generation, conditional display) in vanilla JavaScript demands clear function separation and careful state management (though state is minimal here as it's largely re-calculated on submit).
*   **Caching:** GitHub Pages caching often required thorough browser cache clearing or incognito mode during development to see the latest changes.
*   **Iconography for Dark Themes:** Ensuring PNG icons are visible on dark backgrounds often means having light-colored asset versions, as CSS filters for colorization are not always ideal.

## Future Considerations

While ArcheMorph is quite comprehensive, potential future enhancements could include:
*   More sophisticated "Copy to Clipboard" for sharing.
*   Visualizations of trait scores (e.g., radar charts).
*   A "Lite" version of the quiz with fewer questions.
*   Theming options beyond the current dark theme.

Building ArcheMorph has been a rewarding exercise in creating a feature-rich, client-side application. It demonstrates how much can be achieved with core web technologies when data and logic are thoughtfully structured.

---

*You can explore the ArcheMorph system [here](https://pasx71.github.io/) (assuming this is your link).*
*(Disclaimer: ArcheMorph is for self-exploration and not a clinical diagnostic tool.)*
