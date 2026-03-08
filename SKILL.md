---
name: fix-modal-select
description: Use when a select or dropdown inside a modal, dialog, or overlay renders behind the dialog, escapes to the page layer, or uses a portal that breaks stacking, focus, or interaction.
---

# Fix Modal Select

## Overview
When a dropdown lives inside a dialog, the portal decision matters. Keep the component flexible so normal pages can still use a portal, but dialog-local selects can opt out and stay inside the modal layer.

## Core Pattern
- Add a `portal` prop to the wrapper around `SelectContent`.
- Default `portal` to `true` for normal page usage.
- Render `<SelectPortal v-if="portal">` for the default path.
- Render a local `<SelectContent v-else>` for dialog-contained usage.
- Inside modal flows, pass `:portal="false"` at the call site.

## Quick Reference
- **Wrapper fix**: make portal behavior configurable once in the shared select component.
- **Dialog usage**: use `:portal="false"` only for modal-contained selects.
- **Verification**: confirm the dropdown opens above the overlay, stays clickable, and does not appear in the page layer behind the dialog.

## Common Mistakes
- Hard-coding one behavior for every select in the app.
- Raising `z-index` forever instead of fixing the portal boundary.
- Fixing only visuals while keyboard or pointer interaction still breaks.
- Patching one screen without updating the shared select wrapper.

## Example
Use when the user says: "The switch-project dropdown renders behind the page", "a Select escapes the dialog layer", or "the modal dropdown stacking is wrong".
