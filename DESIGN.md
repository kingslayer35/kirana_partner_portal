---
version: alpha
name: "Valmo Kirana partner"
description: "A practical parcel counter for receiving delivery batches and verifying customer pickups."
colors:
  primary: "#E20750"
  navy: "#231A5C"
  text: "#2B2533"
  muted: "#696475"
  background: "#F6F6F8"
  surface: "#FFFFFF"
  border: "#E8E6EC"
  success: "#19734D"
  warning: "#885B14"
  danger: "#B52B38"
typography:
  ui:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'Segoe UI', Arial, sans-serif"
    fontSize: "15px"
    lineHeight: "1.55"
rounded:
  control: "8px"
  panel: "12px"
spacing:
  page-max: "1240px"
  panel-padding: "24px"
components:
  button:
    padding: "10px 16px"
  card:
    backgroundColor: "#FFFFFF"
---

# Valmo Kirana partner design

## Overview

This is Ramesh General Store's parcel operating dashboard, based on the Meesho DICE 3.0 kirana pickup proposal. The store owner receives a delivery batch, keeps parcels until pickup, scans each parcel again, checks the customer code and collects any remaining COD. The signature is the visible two-scan sequence: receive at the store, then scan at customer handover.

The interface uses a product register: familiar controls, readable amounts and short instructions for someone working at a store counter on a phone or desktop. UI copy is English and existing currency formatting is `en-IN`. Do not add claims of live services, scanners, payment integrations or notifications beyond the existing prototype behavior.

`styles.css` is the sole runtime token and component-style owner. It starts with the shared stylesheet supplied for the three Meesho prototypes and adds only kirana layout/component rules. This file mirrors the accepted runtime values; it does not generate CSS. The original `ST` data remains untouched; rendered status styling uses semantic CSS classes rather than its legacy color literals.

## Colors

PPT navy `#231A5C` gives the wordmark, headings and focus ring their identity. PPT pink `#E20750` marks the primary action and selected controls. `#2B2533` is body text; `#696475` is secondary text. The canvas is `#F6F6F8` and panels are white. Status text has a matching tinted background and an explicit written label.

| Document role | Runtime token | Consumers |
| --- | --- | --- |
| Primary | `--acc` | Primary buttons, active navigation, earnings bars |
| Navy | `--navy` / `--focus` | Headings, wordmark, keyboard focus |
| Text / muted | `--ink` / `--muted` | Body content, labels, secondary copy |
| Background / surface / border | `--bg` / `--surface` / `--line` | Page, cards, tables and separators |
| Success / warning / danger | `--ok` / `--warn` / `--bad` | Status labels and message regions |

## Typography

Use the system sans serif stack from `--font-ui`; no remote font is required. Main headings are 30px on desktop and 27px on small screens. Numbers use tabular figures for easy comparison. Keep order IDs unbroken and allow item names and table headings to wrap naturally. Labels use sentence case.

## Layout

The page has a white brand header, a 208px desktop sidebar and a natural-height workspace within a 1240px frame. At 800px and below, the navigation becomes a compact wrapped set of buttons above the workspace. Dashboard counts become two columns on phones. Pickup form and amount summary sit side by side when space permits, then stack.

Receipt and inventory tables have independent `.table-scroll` wrappers. Only those data regions own horizontal overflow; cards, forms, the application shell and the page remain unconstrained in height. Table content is a fixed small prototype dataset, rendered in full using the existing status filters. No pagination, search or data persistence is added.

## Elevation & Depth

Use white panels and one-pixel borders. No gradients, glass, decorative shadows or large promotional hero regions. Emphasis comes from clear headings, spacing and the amount to collect.

## Shapes

Controls use an 8px radius and panels a 12px radius, mapped to `--radius-control` and `--radius-panel`. Scan step markers and status labels have small corners; rounded shapes must not make static data appear clickable.

## Components

Buttons are at least 44px tall. Pink is the primary action; secondary actions use a white surface and border. Disabled receipt actions preserve the original disabled condition. Selected navigation and order filters have visible state and semantic attributes. All enabled controls have hover, pressed and focus-visible treatments.

The parcel control is a labeled native `<select>`. **The browser and operating system own its open popup, option rendering, geometry and keyboard behavior.** This ownership is accepted; CSS only styles the closed control. Do not replace it with a custom listbox as part of visual cleanup.

Pickup code and parcel fields have explicit label associations. Demo code 4821 remains visible. Payment uses the existing UPI and Cash action buttons with `aria-pressed`. Error feedback uses `role="alert"`; successful receipt and scan feedback use `role="status"`. Tables have captions, column headers and keyboard-focusable scroll regions.

No decorative icons or emoji are used. The earnings bar is an accessible supplement to the written category and amount, and is hidden from assistive technology. Motion is limited to the shared brief hover transition and removed for reduced-motion preferences. Scrollbar colors live in the global stylesheet and defer to forced-colors mode.

## Do's and Don'ts

- Keep the existing parcel data, navigation keys, calculation, scans, validation and mutation order unchanged.
- Put batch identifiers, remaining parcel counts and collection amounts near the action they explain.
- Keep each table's scroll region separate from form and document scrolling.
- Do not add fake live controls, new business rules, a new payment flow or new dependencies.
