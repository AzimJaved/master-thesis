---
name: compare-latex-tikz
description: Compare two screenshots or rendered images of LaTeX/TikZ diagrams ("working image" vs "reference" image) and list all visual and structural divergences. Does not provide code edits.
---

# Visual Divergence Comparison for LaTeX & TikZ Diagrams

This skill compares a **working image** (the current compiled LaTeX / TikZ diagram output) with a **reference image** (the target diagram / reference figure) to systematically detect and list all visual and structural divergences.

> **Important**: This skill focuses strictly on divergence analysis and comparison. Do NOT provide code modifications, replacement snippets, or implementation edits.

## Workflow

### 1. Identify and Read the Images
- Identify the paths for:
  - **Working Image**: Rendered output from current `.tex` / TikZ compilation.
  - **Reference Image**: The target reference diagram or figure.
- Use the `read` tool to load and inspect both image attachments.

### 2. Systematic TikZ & LaTeX Divergence Analysis
Analyze discrepancies across TikZ-specific visual attributes:

1. **Nodes & Geometric Shapes**
   - **Shapes & Radii**: `rectangle`, `circle`, `ellipse`, sharp vs. rounded corners.
   - **Dimensions & Padding**: Width, height, inner padding (`inner sep`), outer padding (`outer sep`).
   - **Border Strokes**: Border presence, stroke width (thin/thick), dash/dot patterns.

2. **Positioning, Layout & Anchors**
   - **Node Placement**: Absolute coordinates vs. relative spacing and positioning.
   - **Anchors & Alignment**: Mismatched attachment points (`north`, `south`, `east`, `west`, etc.).
   - **Matrix & Grid Layouts**: Row/column spacing, vertical/horizontal alignment of parallel nodes.

3. **Edges, Paths & Connectors**
   - **Arrow Heads**: Arrow tip styles (e.g., stealth, standard, latex, bidirectional), tip sizes, double lines.
   - **Routing**: Straight lines, orthogonal routing (`|-` or `-|`), curved paths, bend angles.
   - **Path Labels**: Placement (`above`, `below`, `sloped`, `midway`, `pos=...`), label offset.

4. **Colors, Shading & Fills**
   - Fill colors, tint levels/percentages, shading/gradients, and opacity/transparency.
   - Contrast between node backgrounds and overlaid text.

5. **LaTeX Typography & Mathematical Notation**
   - **Math Formatting**: Math mode vs. text mode, sub/superscripts, symbols, Greek letters, fonts (`\mathbb`, `\mathcal`, `\mathrm`).
   - **Font Size & Weight**: Relative text scaling, bold, italics, small caps.
   - **Text Alignment & Wrapping**: Line breaks, multi-line wrapping, text centering vs. left/right alignment.

6. **Plots, Axes & Legends (if PGFPlots / Data Plots)**
   - Axis limits, tick marks, labels, grid lines, legend position and contents.

### 3. Divergence Report Format

Output only the comparison findings structured as follows:

```markdown
## TikZ / LaTeX Divergence Summary
[Concise summary of overall diagram fidelity and major divergences]

## Detailed Divergences

### 1. Node Shapes, Sizing & Fills
- **[Node / Element]**: [Description of divergence between working and reference]

### 2. Positioning & Layout Alignment
- **[Node / Group]**: [Description of coordinate shifts, spacing, or anchor mismatches]

### 3. Connectors, Arrows & Paths
- **[Edge / Connection]**: [Description of arrow styles, stroke width, curvature, or routing differences]

### 4. Typography & Mathematical Notation
- **[Text / Label]**: [Description of font size, weight, math symbols, casing, or wrapping differences]

### 5. Missing / Extraneous Elements
- **Missing in Working Image**: [Elements present in reference but absent in working image]
- **Extraneous in Working Image**: [Elements present in working image but absent in reference]
```
