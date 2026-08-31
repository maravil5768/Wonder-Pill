# Rendering the mind map

The map is **interactive HTML**, fully expanded, explored by panning and zooming — not a static image and not a progressive reveal. Everything exists at once; the person moves around inside it.

Call `visualize:read_me` with the `diagram` module first (silently — never narrate it). That module is authoritative. Constraints that matter here, and that are stricter than they look:

| Constraint | Consequence |
|---|---|
| No `position: fixed` — ever | The iframe sizes to in-flow content. Fixed elements collapse it to 100px. Controls go in normal flow above the viewport. |
| No `display:none` sections during streaming | Hidden content streams invisibly. Build every node from a JS data array after streaming instead. |
| Scripts run after streaming completes | Safe to render the whole map in JS on load. |
| All colors via CSS variables | `--surface-0/1/2`, `--text-primary/secondary/muted`, `--border`, `--border-strong`, `--bg-accent`. Never hardcode hex — it dies in dark mode. |
| Never rely on color alone | Pair every category with a border style (solid / dashed / dotted) or a text label. |
| No emoji | Tabler outline icons: `<i class="ti ti-plus">`, `ti-minus`, `ti-refresh`. |
| Nothing below 11px | Node text 12–13px. The person zooms; don't shrink type to fit. |
| Sentence case everywhere | Including node labels. |
| Begin with a visually-hidden `<h2 class="sr-only">` | One-sentence summary for screen readers. |

---

## Build it from data, not markup

Hand-writing forty absolutely-positioned divs is how this breaks. Define the map as two arrays and render in JS:

```js
const N = [
  // id, type, x, y, w, title, sub, gut
  ['b1','branch',110,250,260,'what if it fed on the environment?','assumes: durability means resisting it','the hard part is controlling the reaction, not starting it'],
  ['b1t1','tendril',400,250,230,'seawater as a curing agent'],
  ['s1','seed',120,150,240,'roman marine concrete got stronger in seawater'],
  ['x1','scrapped',60,660,250,'what if it floated?','trades a 500-year problem for a 5-year mooring problem'],
];
const E = [ ['topic','b1','solid'], ['s1','b1','dotted'], ['b1','b1t1','solid'], ['b2','b5','cross'] ];
```

Node types and their styling:

| Type | Look |
|---|---|
| `topic` | Solid border, `--surface-2`, 14px medium |
| `branch` | Solid border, `--bg-accent` tint, premise line 11–12px muted above the what-if |
| `tendril` | No border or a single left rule, `--surface-1`, 12px |
| `seed` | **Dotted** border, muted text, small `seed` label |
| `scrapped` | **Dashed** border, 0.5 opacity, title struck through, reason underneath |
| feral branch | Dashed border instead of solid |

---

## Layout: radial but deliberately uneven

A tidy ring of equidistant branches is the thing to avoid — it implies every thread got equal attention, which is false and throws away information.

- Canvas roughly **2000 × 1350**. Topic near the center.
- Place each branch in its own **angular sector**, at whatever radius suits it — 300px for a short thread, 600px for one that ran long. Vary it.
- **Tendrils continue outward** in the same sector, or tangentially when the sector is against a canvas edge.
- **Seeds sit further out than the branch they caused.** The map then reads both inward (why) and outward (where it went).
- **Scrapped nodes float in an unused margin**, connected by nothing or by a faint dotted stub.
- Keep each branch's cluster inside its own zone. Overlap between clusters is the main failure — sketch the zone bounds before placing nodes.

### Cross-links

Two or three, dashed, connecting branches that landed on the same underlying tension. These are the most interesting edges on the map, because a pure tree structurally cannot show convergence.

Cross-links may cross other **lines** — that reads as a web and is fine. They must never pass through a **box**. Check the straight-line path against every node's rectangle before committing; nudge the curve if it clips one.

---

## Interaction

Minimum viable set, in this order of importance:

1. **Drag to pan.** `mousedown`/`mousemove`/`mouseup` on the viewport, updating a `translate()` on the stage. Add `touchstart`/`touchmove` equivalents.
2. **Zoom buttons.** `−` / reset / `+` stepping scale between about 0.3 and 1.4. Skip wheel-zoom: it hijacks page scrolling and irritates more than it helps.
3. **Click a node.** Show its gut-check in a detail strip *below* the viewport (never a floating overlay — `position: fixed` is banned and absolute overlays clip). Highlight the selected node with `--border-strong`.
4. **Go deeper.** A button in the detail strip calling `sendPrompt('Go deeper on the thread: …')` so the person can hand a branch back for a fresh audit.

Structure:

```html
<h2 class="sr-only">…</h2>
<div>controls row — zoom buttons, hint text</div>
<div id="vp" style="height:600px;overflow:hidden;position:relative;cursor:grab">
  <div id="stage" style="position:absolute;transform-origin:0 0;width:2000px;height:1350px">
    <svg>…edges…</svg>
    …node divs…
  </div>
</div>
<div id="detail">…gut-check for the selected node…</div>
```

Initial scale around **0.55** — enough that the shape of the map reads immediately, close enough that labels are legible when they pan in.

---

## Pre-flight checklist

- [ ] No `position: fixed` anywhere; controls and detail strip in normal flow
- [ ] Every color from a CSS variable; test mentally against a near-black background
- [ ] Every category distinguishable without color (border style or label)
- [ ] No cross-link or edge passes through a node box
- [ ] No two node boxes overlap
- [ ] Branch radii and depths are visibly uneven
- [ ] Seeds sit outside their branches; scrapped nodes are detached
- [ ] Every branch shows both its premise and its what-if
- [ ] Legend present, matching the border styles actually used
- [ ] Drag, zoom, and click all work after streaming completes
- [ ] Stage dimensions large enough that no node is clipped at the canvas edge
