# Copilot instructions

## Project overview

This is a dependency-free browser quiz implemented entirely in `index.html`. The file contains the HTML structure, all CSS, the question data, and the quiz state/interaction logic. It is intentionally runnable as a local file with no server, build step, package manager, or external assets.

The UI has three mutually exclusive states:

- `#start-screen`: introductory screen and mission start control.
- `#quiz-screen`: question, answer buttons, progress bar, score, feedback, and next control.
- `#results-screen`: final score, emoji reaction, score-specific message, celebration styling for scores of 8 or higher, and restart control.

Quiz state is held in the script-level `currentQuestion` and `score` variables. `showQuestion()` renders the current question from the `questions` array, `selectAnswer()` disables all answer buttons and applies the correct/incorrect feedback state, and `showResults()` switches to the result screen and selects the corresponding message. When changing quiz behavior, update these state transitions together rather than adding separate state sources.

## Commands and validation

There are no project-defined build, test, lint, or dependency-install commands. Do not introduce a toolchain for routine changes.

Run the page locally on macOS with:

```sh
open index.html
```

For a focused manual smoke test, open `index.html` directly in a browser and verify one correct answer, one incorrect answer, score/progress updates, the next-question flow, the final result screen, and restart. Keyboard testing should use `Tab`, `Enter`, and `Space`; answer controls and navigation are native `<button>` elements.

When working in the Copilot app, prefer the integrated browser with the `file:///.../index.html` URL so the no-server requirement remains covered. There is no single automated test command; a single manual scenario is the smallest available test.

## Implementation conventions

- Keep the application self-contained in `index.html`; avoid external libraries, fonts, images, network requests, and separate JS/CSS files unless the project direction explicitly changes.
- Preserve the existing screen/state model and use the existing IDs (`start-screen`, `quiz-screen`, `results-screen`, `answers`, `feedback`, `next-button`, and related score/progress IDs) when wiring UI changes.
- Add questions as objects in the `questions` array with `question`, `options`, and zero-based `answer` fields. Keep exactly four options per question unless the rendering and accessibility logic are intentionally updated together.
- Use `textContent` for dynamic text. The current answer rendering uses fixed markup for the option letter and text; do not interpolate untrusted content into HTML.
- Keep visual values in the existing CSS custom properties and extend both the default theme and `@media (prefers-color-scheme: dark)` theme when adding colors.
- Preserve responsive behavior: the main app is a narrow centered column, cards use fluid padding, and the existing small-screen media query protects the mission-control header.
- Respect accessibility behavior already present: use native buttons, retain `type="button"`, keep `aria-live` feedback, update the progress bar's `aria-valuenow`, and provide visible `:focus-visible` styles.
- Preserve `@media (prefers-reduced-motion: reduce)` when adding animations or transitions. Decorative motion must stop or become effectively instant in reduced-motion mode.
- Keep correct answers green and incorrect answers red. The incorrect state intentionally uses the `shake` animation; changes to feedback should not remove the visual distinction or the explanatory message.
- Keep the automatic light/dark behavior driven by `color-scheme` and `prefers-color-scheme`; do not replace it with a manual theme toggle without an explicit product request.
