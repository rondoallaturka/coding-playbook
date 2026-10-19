---
name: building-ui
description: Checks that user-facing UI works for the person using it, covering loading, empty, and error states, feedback, layout at different screen sizes, accessibility, and consistency with the existing design. Use when building or changing screens, pages, components, forms, or flows that a user sees, and before calling UI work done.
---

# Building UI

Tests and a clean build say little about whether a UI works for the person using it. UI work is done when you've looked at the result and it handles more than the success path.

## Look at what you built

- Run the app and view the change, using whatever the project or environment provides: a browser automation tool, Playwright screenshots, Storybook, or visual tests.
- If you were given a design or screenshot, compare the result against it, list the differences, and fix them.
- Check a narrow, phone-sized width as well as desktop.
- If you can't render the UI in this environment, say so and list what someone should check by hand.

## Handle every state

For each screen or component you touched:

- **Loading**: something shows while waiting, and the layout doesn't jump when the data arrives.
- **Empty**: a short message and, where it helps, the next step, instead of a blank area.
- **Error**: says what went wrong in the user's terms and how to recover, without losing what they entered.
- **Feedback**: every action gets a visible response, and buttons that start work can't be submitted twice.
- **Real content**: long names, many items, missing images, large numbers, and other languages if the app supports them.
- **Destructive actions**: offer undo where you can; otherwise ask for confirmation.
- **Keyboard and accessibility**: everything is reachable by keyboard with visible focus, inputs and icon buttons have labels, and text has enough contrast.

## Fit the product

- Use the project's existing components, styles, and design tokens before creating new ones. Match spacing, typography, and the tone of existing copy.
- Write UI text for the user: plain words, no internal names, and no bare error codes.

## Fresh-eyes review for new screens and flows

For a new screen or multi-step flow, show it to the person you're working with, ideally in a tool that lets them comment on specific elements, and ask what's confusing, missing, or inconsistent. Fix what stops the user from completing their task; treat the rest as suggestions.
