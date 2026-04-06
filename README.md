# Portfolio — Interactive Network Landing Page

A single-page portfolio that uses a **cursor-reactive node network** as its primary navigation. Each node in the foreground network is a clickable link to a dedicated section page.

## How it works

| Layer | Description |
|-------|-------------|
| **Background mesh** | ~100 invisible nodes connected by faint edges; subtle drift and cursor-reactivity. |
| **Foreground network** | 8 named nav-nodes with physics-based motion, spring forces, cursor repulsion, and node–node repulsion. |

Both layers run on separate `<canvas>` elements via `requestAnimationFrame`.

---

## Customising nodes

Open `index.html` and edit the `NAV_NODES` array near the top of the `<script>` block:

```js
var NAV_NODES = [
  { label: 'Contact',     href: 'contact.html'     },
  { label: 'Passion',     href: 'passion.html'     },
  // add / remove entries here
];
```

Add a matching entry to `HOME_RATIOS` (viewport fractions `rx`/`ry` in [0,1]) and `NAV_EDGES` (index pairs) to position and connect the new node.

---

## Customising themes

Two themes are built in — **dark** (default) and **light** (white background, red edges, thick black node borders).

The theme toggle button (◐, top-right) switches between them at runtime.

To change colours, edit the `THEMES` object:

```js
var THEMES = {
  dark: {
    bgEdgeRGB: [255,255,255], bgEdgeMaxA: 0.038,  // background mesh opacity
    fgEdge:    'rgba(210,210,210,0.22)',            // foreground edge colour
    // ...
  },
  light: {
    fgEdge:    'rgba(180,0,0,0.42)',               // red edges
    nodeStrokeW: 3,                                // thick black border
    // ...
  },
};
```

---

## Adjusting physics

All physics constants live in the `CFG` object inside `index.html`:

| Key | Effect |
|-----|--------|
| `fgSpringK` | How strongly nodes snap back to their home positions |
| `fgNoise` | Amount of random drift per frame |
| `fgRepelRCursor` / `fgRepelFCursor` | Cursor repulsion radius and force |
| `fgRepelRNode` / `fgRepelFNode` | Node–node repulsion |
| `fgDamping` | Velocity damping (closer to 1 = more floaty) |
| `bgCount` | Number of background mesh nodes (affects density) |
| `bgConnectDist` | Max distance for background edges |

---

## Section pages

| Page | File |
|------|------|
| Contact | `contact.html` |
| Passion | `passion.html` |
| Work | `work.html` |
| Subject | `subject.html` |
| Note | `note.html` |
| Photographs | `photographs.html` |
| Articles | `articles.html` |
| Blogs | `blogs.html` |

Each page has a **← Home** link that returns to the network landing page.

---

## Accessibility

- The `prefers-reduced-motion` media query is respected: when enabled, all physics motion stops and nodes remain at their home positions.
- Theme colours meet a minimum contrast ratio for legibility.
