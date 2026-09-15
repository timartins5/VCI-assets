# VCI-assets

Shared CSS and brand assets for VCI internal web apps (Google Apps Script,
HTML Service). Served via GitHub Pages.

## Current file

https://timartins5.github.io/VCI-assets/vci-shared-v1.css

Add to a tool's `<head>`:

    <link rel="stylesheet" href="https://timartins5.github.io/VCI-assets/vci-shared-v1.css">

## Versioning

The version is in the filename. Published files are never edited in place.

Apps Script serves web apps inside an iframe on a googleusercontent.com
origin and caches aggressively. A changed file at an unchanged URL will not
reliably reach users, and users will not hard-refresh. Publishing a new
filename is the only cache-bust that is guaranteed to work.

To change a token: copy to `vci-shared-v2.css`, edit, publish, then update
each consuming tool's `<link>` and redeploy it. Keep the old file in place
so tools not yet migrated keep working.

## What v1 contains

Design tokens only — brand colors, surfaces, text, borders, elevation,
radius, spacing, semantic status colors, and the Open Sans import.

Every value was extracted from CSS already in use across the tools, not
invented. Where tools agreed, that value won. Where they disagreed, the
majority won, and the decision is commented inline in the stylesheet.

## What v1 deliberately does not contain

**Components.** A September 2026 inventory across six tools found:

- Toast and spinner: two internally-consistent families. Pest Vendor and
  TPO Lender Lookup are byte-identical to each other; Company Directory and
  Logins & Links are byte-identical to each other. The two families differ.
  TPO Escalations has a richer toast (stacking, semantic variants, dismiss)
  that is a superset, not a conflict.
- Modal shell: structurally shared across five of six tools, differing in
  backdrop opacity (.35/.45/.65), z-index (500/1000/9999), corner radius,
  and whether there is an entry animation.
- Buttons: the most-repeated component with the least agreement. Four
  border-radius conventions (999px pill, 8px, ~14px token, 2px sharp),
  three class-naming approaches, and Turn Time's all-caps sharp-corner
  style, which is a different visual language rather than a variant.
- Badges, empty states, tables, form inputs: no shared class names at all.

Components land in v2, after the button question is decided. Shipping a
component library built on an unresolved disagreement means every tool
either conforms or works around it, and the ones that work around it are
the reason the drift existed in the first place.

## Adoption

Tools adopt incrementally. Link the stylesheet, delete the local `:root`
block, keep everything else. The compatibility aliases at the bottom of the
stylesheet cover the three different naming conventions in use, so a tool
does not have to be renamed before it can consume this.

Expect two visible changes on adoption:

- Pest Vendor Tool's brand red shifts from `#ae2643` to `#AD2542`. Visually
  indistinguishable, but it is a real change.
- Any tool using a non-standard hover red picks up `#8F1E37`.
