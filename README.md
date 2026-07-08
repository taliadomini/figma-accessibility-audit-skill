# Figma Accessibility Audit Skill

A custom Figma agent skill that audits a frame against five WCAG 2.2
success criteria: target size, use of color alone, meaningful
sequence, accessible naming, and contrast. Point it at a frame and it
returns a criterion-by-criterion report with a rollup summary.

## What it checks

1. **Target Size**: WCAG 2.5.8 (AA, 24x24px) and WCAG 2.5.5 (AAA,
   44x44px touch target), reported side by side.
2. **Use of Color Alone**: WCAG 1.4.1.
3. **Meaningful Sequence**: WCAG 1.3.2, comparing visual reading
   order to layer order.
4. **Name, Role, Value**: WCAG 4.1.2, flagging generic auto-named
   layers that would produce empty accessible labels in code.
5. **Contrast**: WCAG 1.4.3 (text) and 1.4.11 (non-text UI), computed
   from actual fill values, not estimated.

## Usage

Run the skill against a Figma frame. It reports PASS / FAIL / NEEDS
HUMAN REVIEW per criterion, lists every violation instance (capped at
10 per category, with an explicit count if there are more), and links
each finding back to the flagged layer.

## On reliability: read this before trusting a single run

This skill has been run repeatedly against the same unchanged frame,
specifically to test whether an AI agent's accessibility judgment is
consistent. It isn't, on every criterion equally.

**What stayed consistent across runs:**
- Contrast ratio math. Nested opacity compositing resolved correctly
  and reproduced closely across runs.
- Meaningful Sequence: reliable both times tested.
- Overall FAIL/PASS direction on Name, Role, Value.

**What did not stay consistent:**
- **Use of Color Alone flipped outright** between two runs on the
  identical element. One run judged a filled-vs-unfilled toggle state
  as color alone (FAIL); the next judged the same visual distinction
  as sufficient non-color signal (PASS).
- **The WCAG 2.5.8 spacing exception was applied inconsistently.**
  Several elements were marked as failing the spacing exception in one
  run and passing via that same exception in the next.
- **Element counts varied** between runs on a static frame (15 vs. 20
  interactive elements identified), which means even the elements
  being evaluated aren't guaranteed to match run over run, not just
  the verdicts on them.

The practical takeaway: this skill is reliable for objective,
measurable checks (contrast math, layer order, literal name strings)
and unreliable for anything requiring visual judgment (is this color
change enough on its own, does this spacing exception apply). Treat
single-run output as a starting point for human review, not a final
verdict, particularly on criteria 1 and 2.

## Why this exists

Built as part of a broader series of experiments testing how AI
agents perform on real design tasks, specifically where the reliable
edge of automated judgment sits. The dividing line here (solid on
computation, shaky on visual and contextual judgment) shows up
repeatedly in AI-assisted design tooling and is worth designing around
rather than assuming away.
