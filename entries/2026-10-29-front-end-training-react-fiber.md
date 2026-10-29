# Front-End Training: React Fiber, Read from the Source

Today's deep dive on
[Front-End Training](https://chalidade.github.io/front-end-training/) (PR #16),
in Indonesian and English, walks through React's own source code.

- The `FiberNode` structure, the work loop and `shouldYield`, `beginWork` and
  bailouts, how children are reconciled and what `key` really does, hooks as a
  linked list, lanes, and the commit phase
- The experiments were checked against React 19.3.1
- Linked from stage 07, the deep-dive index and the sidebar

**Lesson:** "hooks can't go inside an if" makes sense once you see that hooks
are a linked list read back in call order.
