# Front-End Training: A Module Bundler From Scratch

Today's deep dive on
[Front-End Training](https://chalidade.github.io/front-end-training/), in
Indonesian and English.

- A bundler in about 60 lines with acorn: parse, resolve, build the graph,
  write a runtime
- Circular imports in CommonJS versus ES module live bindings
- Scope hoisting, tree shaking and `sideEffects`, code splitting and content
  hashes, and why a dev server works differently from a build
- Experiments checked against acorn 8.19.0, rollup 4.65.0 and esbuild 0.27.7

**Lesson:** a bundler is a graph walk plus a tiny runtime. Everything else is
about making that graph smaller.
