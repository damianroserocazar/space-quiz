# Copilot instructions

## Project structure and architecture

- This is a standalone, dependency-free web quiz. The complete application lives in the root `index.html`; markup, CSS, quiz data, and JavaScript are intentionally kept together so the file can be opened directly without a server or build step.
- The JavaScript `questions` array is the source of quiz content. `showQuestion()` renders each question and its options, `selectAnswer()` handles feedback, score, and progress, and `showResult()` selects the final reaction based on the score. The intro, quiz, and result are separate views toggled with the `hidden` attribute.
- `currentQuestion` and `score` are the quiz state. Starting initializes the first question; the next action advances or finishes the quiz; replay resets the score, question index, and progress.
- The UI is in Spanish. Keep visible copy, question content, categories, and explanatory facts in Spanish.

## Commands and checks

- There is no package manifest, build, lint, or automated test runner configured.
- To run the app, open `index.html` directly in a browser.
- For a focused manual check, start the quiz, answer one question incorrectly and another correctly, and verify that options become disabled, the right answer is revealed, feedback is announced, and only a correct answer increments the score. Check progress after each response, complete all ten questions, and use replay to confirm state resets.
- Check keyboard focus as views and questions change, and check the light/dark and reduced-motion preferences in the browser.
- There is no CLI single-test command; use the manual browser check above for an isolated behavior check.

## Code conventions

- Keep the app self-contained in `index.html`; do not introduce a framework, external asset, server requirement, or dependency without a project-level need.
- Add quiz entries using the existing `{ category, text, options, answer, fact }` shape. `answer` is a zero-based index into `options`.
- The progress bar tracks questions answered, whether the response was right or wrong; the score tracks correct answers only. Keep these meanings consistent when changing quiz behavior.
- Result copy and emoji are selected by score thresholds inside `showResult()`. Update those branches if changing the number of questions or scoring scale.
- Use the existing CSS custom properties for colors and surfaces. Define theme-specific values in the `prefers-color-scheme: dark` override so additions work in both color schemes.
- Preserve the accessible interaction pattern: semantic headings and native buttons, a labelled progress bar, live score and feedback announcements, visible keyboard focus, and focus transfer to the question, next action, or replay action as views change.
- Keep decorative elements hidden from assistive technology where appropriate, and keep motion effects compatible with the existing `prefers-reduced-motion` override.
