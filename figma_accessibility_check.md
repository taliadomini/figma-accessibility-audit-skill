---
name: accessibility-check
description: Evaluate components against accessibility standards
---

You are auditing a Figma frame against five WCAG 2.2 success criteria.
For each criterion, report PASS or FAIL, and explain what you observed
that led to that conclusion. Be specific about which layer or element
triggered each finding, and include a direct link to it (see "Linking
to frames" below).

Do not estimate dimensions, spacing, or color values by eye. Read
actual values from the layer properties.

1. TARGET SIZE (WCAG 2.5.8, Level AA / WCAG 2.5.5, Level AAA)
Interactive elements (buttons, icons, form controls, links) must be at
least 24x24px, OR have at least 24px of spacing from any adjacent
interactive element. Measure actual frame dimensions and spacing —
this is the AA baseline (WCAG 2.5.8) and applies regardless of
platform.

Separately, report whether the same element also clears 44x44px. This
isn't a distinct WCAG AA rule — it's the AAA enhanced target size
(2.5.8) and it's also the convention Apple and Google use for
touch-target guidance. Rather than requiring you to specify mobile or
web up front, report both for every interactive element: "24x24 AA:
PASS/FAIL" and "44x44 touch target: PASS/FAIL." That gives a complete
picture regardless of the surface.

2. USE OF COLOR ALONE (WCAG 1.4.1, Level A)
Information, state, or required action must not be conveyed by color
alone. Check specifically for: error states marked only by a colored
border or background with no icon or text; status indicators (active/
inactive/pending, etc.) distinguished only by dot or fill color with no
label; required form fields marked only in red with no symbol or text.

3. MEANINGFUL SEQUENCE (WCAG 1.3.2, Level A)
Compare the visual reading order (left-to-right, top-to-bottom) of the
frame against the layer order in the Layers panel. Flag any case where
they diverge — this matters because screen readers traverse content in
layer/DOM order, not visual position.

4. NAME, ROLE, VALUE / accessible naming (WCAG 4.1.2, Level A)
Check whether icon-only buttons and interactive elements have
descriptive layer names (e.g. "Close dialog," "Delete row") versus
generic auto-generated names (e.g. "Vector 47," "Group 12," "Frame 3").
Generic names indicate the equivalent of a missing accessible name in
production code.

5. CONTRAST (WCAG 1.4.3 and 1.4.11, Level AA)
Extract the actual fill values (hex or RGBA) for text against its
background, and for non-text UI components (icon fills, borders, focus
indicators, form field outlines) against their adjacent color.
Calculate the contrast ratio from relative luminance — don't estimate
visually.

- Text: normal text needs ≥4.5:1. Large text (18pt/24px+ regular, or
  14pt/18.66px+ bold) needs ≥3:1.
- Non-text UI components and graphical objects required to understand
  content or operate the interface (icons, borders, focus states) need
  ≥3:1 against adjacent colors. Exempt: inactive/disabled components,
  decorative elements, logos.

Report the computed ratio and the threshold that applies, not just a
verdict.

For each of the five criteria, end with a one-line summary: PASS /
FAIL / NEEDS HUMAN REVIEW (use this last option if the frame doesn't
give you enough information to judge confidently, rather than
guessing).

## Reporting every violation, not a sample

When a criterion fails in multiple places, list every instance — not a
representative few. If there are more than 10 instances of the same
violation type, list the first 10 with exact layer names/paths, then
state the total count explicitly: "Showing 10 of 23 target size
violations." Never stop counting silently, and never let the report
imply completeness you haven't confirmed.

## Overall summary

After the five individual criteria, close with a rollup table, one row
per criterion, two columns: the criterion (with its WCAG number) and
the verdict plus a one-line reason. Include this table every time —
it's part of the required output, not an optional recap.

## Linking to frames

For every flagged element, reference the actual layer/node object —
not its name typed as plain text. When you pull element data from
Figma (via a design inspection or context call), carry that same node
reference through into the finding itself; that's what renders it as
a clickable link back to the layer. Do this for every finding, not
only the ones that happen to still have the reference on hand.

If at any point you only have a plain-text name and no underlying
node reference to attach, say so explicitly ("layer name only, no
link available") rather than presenting it as if it were linked.
