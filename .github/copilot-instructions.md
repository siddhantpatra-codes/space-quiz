# SpaceQuiz

Single-file space exploration quiz: everything (HTML, CSS, JS) lives in `index.html`. No build, no package manager, no tests, no linter, no server. Open the file directly (`file://…/index.html`) to run it.

## Architecture

- **Data:** `Q` array of `[question, [4 options], correctIndex]`. Add or edit questions there; the "10 questions" count and progress bar derive from `Q.length`, but the results emoji thresholds in `end()` assume percentages, so they adapt automatically.
- **State:** two globals, `i` (current question) and `score`.
- **Rendering:** `show()` rebuilds `#app` via `innerHTML` for each question; `end()` renders the results screen. Question/option text is set with `textContent`, not interpolated into HTML — keep it that way.
- **Feedback:** answering adds `.ok` (green, pop animation) or `.bad` (red, shake animation) to the option; on a wrong pick the correct option also gets `.ok`. Options are real `<button>`s and are disabled after answering; focus moves to the Next button so the quiz is keyboard-operable.

## Conventions

- Theming is via CSS variables on `:root`, overridden in `@media (prefers-color-scheme: dark)`. The page background is always a dark starfield (stacked `radial-gradient`s on `body`); only the card follows light/dark.
- Keep body font at 14–16px, sans-serif system stack, and the card at `max-width: 520px` centered.
- No external dependencies, fonts, or network requests.

## Verifying changes

There is no test suite. Verify in the integrated browser: reload, click a correct and a wrong answer, and check the results screen. Screenshots taken immediately after a click can show stale pre-repaint state, so take a second one before concluding something is broken.
