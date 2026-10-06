# A Walkable Home Page in Plain DOM

The [tools site](https://chalidade.github.io/tools/) opens with a top-down town
you walk with the keyboard. There is no canvas and no game engine: it is React +
Tailwind divs and inline SVG, so the art uses the same theme tokens and dark mode
as the rest of the site. Code:
[`src/components/playground/`](https://github.com/chalidade/tools/tree/main/src/components/playground).

## React draws, the loop moves
React renders a scene once: ground, buildings, trees, people. After that, a single
`requestAnimationFrame` loop owns everything that moves, and it never calls
`setState` per frame. It writes `style.transform` on refs and sets data attributes
like `data-walking` or `data-dir="up"`. CSS reacts to those: legs step, arms swing,
and you see the back of the head when walking up.

React state changes only when the UI has to: who is in reach, the open dialog, the
current scene, the visited stamps. That happens a few times a minute, not 60 times
a second.

## Depth is just y
Every sprite is anchored at its feet, and its `z-index` is its y coordinate. A
person standing above a tree is drawn behind it, and below it in front, with no
sorting code. The same trick makes tall grass work: each 26 px grass tile has
`z-index` = its bottom edge. Whoever stands inside that tile is drawn behind it,
and the blades cover their feet.

Buildings only block their lower part, the walls. The roof area stays walkable,
so you can pass behind a building and it hides you.

## Collision and click-to-walk
- Solids are circles (trees, the fountain, keepers) and rectangles (walls,
  benches). Each frame the body is pushed out along the shortest way, then clamped
  inside the scene. That is enough for sliding along walls.
- Walking in a straight line toward a click gets stuck on the first tree, so clicks
  use A* on a 20 px grid. A cell is blocked if a body of the player's radius
  (+2 px) centred there would overlap a solid. The grid is built once per scene and
  cached in a `WeakMap`.
- The raw cell path zigzags. Straighten it by jumping to the farthest waypoint the
  body can reach in a straight line, sampling the segment every 8 px.
- When a target is inside something (you clicked a house), snap to the nearest
  open cell. Give up if the player hasn't moved for half a second.

## Gotchas
- **State updaters can be skipped.** Opening a tool changes the hash and unmounts
  the page. A `localStorage` write inside `setVisited(prev => …)` never ran. Do the
  side effect first, then set state.
- **`overflow: hidden` still scrolls.** Browsers can scroll it from code; a tap
  that scrolled an element into view slid the whole map sideways on phones.
  `overflow: clip` cannot be scrolled at all.
- **Don't steal the arrow keys.** The world only listens while at least 45% of it
  is on screen (an `IntersectionObserver`), so arrows still scroll the rest of the
  page. Typing in an input is never intercepted.
- **Don't fix one layer with z-index.** I lifted talking residents above
  everything so their speech bubble wouldn't hide behind trees. That drew a whole
  person in front of a building they were standing behind. Depth has one rule
  (y), so keep it that way.

## Keep it honest
The map is `aria-hidden` with no tab stops. The searchable tool grid below it is
the real interface, and the town is a fun front door to it. Ambient motion (smoke,
ripples, clouds) is CSS and switches off under `prefers-reduced-motion`.
