# PRD: Add Item to Specific Section in Proposals

## Problem
When users click "+ Add Item" in a Roofr Proposal, the item is always appended to the bottom of the full list. If the user wants it in a specific section (e.g., "Atlas"), they must drag it — sometimes across many rows — creating unnecessary friction during proposal building.

## Users
Roofr users actively building or editing Proposals, particularly those with multi-section proposals (3+ sections) where drag distance is greatest.

## Goals
- Allow users to add an item directly into a target section without drag-and-drop
- Reduce friction in proposal editing flow
- Keep the experience lightweight — adding an item should still feel fast

## Non-goals
- Reordering sections themselves (out of scope)
- Changing how items behave when there are no sections (they continue to append to the bottom)

## Solution — Two directions to prototype

**Option A: Per-section inline "+ Add Item"**
Each section header row gets its own "+ Add Item" affordance. Clicking it inserts a new item directly beneath the last item in that section. The global "+ Add Item" at the bottom remains for unsectioned items.

**Option B: Section picker on "+ Add Item"**
The global "+ Add Item" button triggers a small dropdown or modal asking "Add to which section?" with the list of current sections + "No section" as options. Item is inserted at the bottom of the chosen section.

## Edge cases
- **No sections exist** — current behavior preserved; item appends to end of list
- **Empty section** — item becomes the first item in that section
- **Long section list** — Option B picker needs to scroll gracefully if there are many sections
- **Single section** — Option B feels like unnecessary overhead; Option A may be more natural

## Open questions
- Does the new item open inline for editing immediately after insertion, or does it just appear and wait?
- Should the per-section affordance (Option A) always be visible, or only on hover of the section header?
