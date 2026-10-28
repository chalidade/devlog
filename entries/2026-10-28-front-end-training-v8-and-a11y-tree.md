# Front-End Training: How V8 Runs Your Code, and How a Screen Reader Reads Your Page

Two daily deep dives on
[Front-End Training](https://chalidade.github.io/front-end-training/), one on
27 October and one on 28 October, each in Indonesian and English and each with
six experiments to try yourself.

- **How V8 works** (PR #13): lazy parsing, the Ignition interpreter and feedback
  vectors, hidden classes, inline caches, elements kinds, and speculative
  optimisation with deopts. The experiments were run on Node 22. Linked from
  stages 04 and 16
- **The accessibility tree and how screen readers work** (PR #15): how the DOM
  maps to the accessibility tree (HTML-AAM), how an element's accessible name is
  computed, where ARIA stops helping, a screen reader's browse mode, live regions
  and focus management. The example trees come from Chromium's own output.
  Linked from stages 02 and 15

**Lesson:** both topics are things the browser does with my code that I never
see directly. The experiments make them visible: a deopt you can trigger, a
tree you can print.
