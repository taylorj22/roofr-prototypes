# Template Page Redesign

**Product area:** Proposals > Templates tab
**Status:** Draft — May 6, 2026

---

## Problem

The Templates page is a flat, unorganized grid. There's no way to distinguish a proposal template from a material order template except by name — users are literally calling things "My ABC template for MOs" to tell them apart. A new capability now lets users create a Material Order directly from a template (skipping the proposal step), but the UI doesn't reflect this at all. The page needs structure and metadata to support this and to scale as template libraries grow.

---

## Users & jobs to be done

**Admin / owner** setting up the account's template library. They're the ones creating, organizing, and maintaining templates. They need to know what each template is for without opening it.

**Sales rep or team member** picking a template to start a proposal or order. They need to find the right template fast, and understand at a glance what it includes.

**Trigger:** user starts a new proposal or material order and needs a starting point. Or an admin is reviewing and cleaning up the template library.

**Today's workaround:** naming conventions and memory. "My ABC template for MOs," "Residential — INSURANCE," etc. Doesn't scale. Falls apart when multiple people share the library.

---

## What we're building

A redesigned Templates tab with three changes:

1. **Folder organization.** A left-panel folder sidebar with user-managed folders. Defaults to "Proposal Templates" and "Material Order Templates." Admins can create, rename, and delete folders. Team members can browse and use, but not manage.

2. **Template type property.** Each template is explicitly typed as either a Proposal Template or a Material Order Template. This property drives the card design and folder placement.

3. **Richer template cards.** Cards show section tags (with the Estimate section visually highlighted as the one that carries into Material Orders). Proposal templates keep their cover image thumbnail. MO templates show a generic icon instead.

---

## Non-goals

- New template creation flow (what type are you creating, blank vs. template) — out of scope.
- "Use" flow detail (the modal to select job and create proposal vs. MO) — out of scope.
- Mobile-specific design.
- Jumpstart / onboarding templates (covered in the progressive onboarding PRD).

---

## User flow

### Browsing

1. User navigates to Proposals > Templates.
2. Page loads with the folder sidebar on the left, template grid on the right.
3. Default view: "All Templates" folder selected, all templates visible.
4. User clicks "Proposal Templates" or "Material Order Templates" (or a custom folder) to filter.
5. User finds the template they want.
6. Clicking a card opens the template editor (Edit).
7. Hovering a card reveals Edit and Use buttons.

### Using a template

1. User clicks Use on a template card.
2. (Out of scope for this PRD — covered separately.) Modal asks: create a Proposal or Material Order? Select associated job. Confirm.

### Managing folders (admin only)

1. Admin sees a "+ New folder" option at the bottom of the folder list.
2. Admin clicks it, types a folder name inline, hits Enter.
3. Folder appears in the sidebar.
4. Admin can rename or delete folders via a `...` menu on each folder row.
5. Deleting a folder doesn't delete the templates inside — they move to "All Templates" (unfiled).

### Moving a template to a folder

1. User opens the `...` menu on a template card.
2. Selects "Move to folder."
3. A picker shows available folders.
4. Template moves immediately.

### Setting a template's type (Proposal vs. MO)

1. Inside the template editor, a property (likely in a settings panel or header) lets the user designate the template as Proposal or Material Order.
2. Setting it to MO swaps the card thumbnail to an icon and applies the "Material Order" badge.
3. This is the primary signal used for folder organization and card rendering.

---

## Key behaviors

### Folder sidebar

- Two default folders: **Proposal Templates** and **Material Order Templates**.
- "All Templates" is always the first item (not a real folder, just the unfiltered view with a count).
- Folders show a template count badge.
- Admin-only actions: create folder, rename folder, delete folder.
- Deleting a non-empty folder: templates become unfiled (appear in All Templates only), not deleted.
- Folder order: drag to reorder (admin only).

### Template cards

| Property | Proposal Template | Material Order Template |
|---|---|---|
| Thumbnail | Cover page image | Generic document icon |
| Badge | None (or "Proposal" if needed for clarity) | "Material Order" badge |
| Sections shown | All sections, Estimate highlighted | Estimate only (it's all that matters) |
| `...` menu | Edit, Duplicate, Move to folder, Delete | Same |

### Estimate section highlight

The Estimate section pill on each card is visually distinct (color-coded) to communicate that it's the section that carries into Material Orders. This is educational for users who don't know the relationship yet. A small tooltip or legend on the page explains it.

### Card `...` menu

- **Edit** — opens the template editor.
- **Duplicate** — creates a copy in the same folder, named "Copy of [Name]."
- **Move to folder** — opens folder picker.
- **Delete** — confirmation required ("This can't be undone").

### Permissions

Mirrors the File Manager model:
- **Admin:** full control. Create/rename/delete folders, edit/delete/move templates.
- **Team member:** read + use only. Can browse all templates, click Use. Cannot create folders, cannot delete or move templates.

---

## Open questions

| # | Question |
|---|---|
| 1 | Where does the MO type property live in the template editor? (Header toggle, sidebar settings panel, a prompt on first save?) |
| 2 | Should existing templates default to "Proposal Template" type on rollout, or stay untyped until the user sets it? |
| 3 | What happens to the GBB/multi-option badge that currently exists on some cards (the stacked layers icon)? Does that coexist with the new section tags, or get replaced? |
| 4 | If a user deletes the "Material Order Templates" default folder, should it be re-createable? Or is that folder protected? |
| 5 | Does the section tag list come from the actual template content (dynamic) or is it manually set on the template? |
| 6 | Is there a max number of folders, or is it unlimited? |
