# weeknoo: Free AI That Runs on Your Own Laptop, and What It Costs in Seconds

Every weeknoo site now carries `@/lib/ai`, a chat client for
[Ollama](https://ollama.com/) running on the visitor's own machine. Then I built
`ask`, a question-and-answer site, as its first real user, and spent most of the
day measuring.

- **Ollama only, no hosted provider.** The first version also had Hugging Face
  as a fallback. I removed it within ten minutes: it bills per token and needs a
  key, which isn't what "free AI" means. What's left costs nothing, needs no
  account and works offline
- **Reasoning stays separate from the answer.** `reasoning.ts` splits
  `<think>…</think>` out of the reply, also while streaming, when a tag gets cut
  across two chunks. The `ask` UI shows the thinking in a panel that opens while
  the model thinks and closes when the answer starts
- **`think: false` is a trap.** Tested on qwen3:4b with Ollama 0.33.2: it doesn't
  stop the model from thinking, it only stops Ollama from labelling it. The
  thinking then lands in the answer with no tags and can't be split out.
  `/no_think` was ignored too
- **Speed on a CPU laptop** was 8.5 words a second with free RAM and 2.8 once it
  started swapping, so one answer takes 30 to 120 seconds. That's why streaming
  is required: a non-streaming call looks frozen
- **The system prompt mattered more than I expected.** Without an Indonesian
  one, qwen3 thought in English and kept re-checking itself: "capital of West
  Java" ran 103 seconds with no answer. With it: 17 seconds, "Bandung"
- **Overthinking a greeting.** "kamu bisa apa saja" (what can you do) took 384
  seconds, 4,980 characters of thinking for an 86-character answer. A stricter
  prompt cut the thinking about 4×, but never to zero. What worked was picking
  a non-reasoning model automatically when one is installed: qwen3:4b-instruct
  answered the same question in 11 seconds
- **History on the device** with Dexie: the answer row is written at the start
  and overwritten every 1.5 seconds rather than once per chunk (an answer can be
  300 chunks), and every write is wrapped so a failing IndexedDB (private mode)
  never kills the conversation
- **Markdown** with react-markdown, remark-gfm and highlight.js, lazy-loaded:
  highlight.js alone is ~320 kB, so it's a separate chunk fetched with the first
  answer, and the main bundle stays 333 kB
- **Images** for vision models. The model's `capabilities` come from Ollama
  instead of guessing from its name, because a text model accepts an image and
  ignores it without saying so. I downscale photos to 1024 px, and my first
  comment claimed it saved time. Measured with qwen2.5vl:3b, 1024 px and 640 px
  both came to 1,098 tokens and ~250 seconds, because Ollama resizes the image
  itself. It only saves storage, so I corrected the comment
- A vision model sends nothing until it has read the image (up to 4 minutes),
  so the screen now shows a running "processing… N seconds" counter

**Lesson:** with a local model the bottleneck is time, and you only learn where
it goes by measuring. Two of my assumptions today (that `think: false` turns
thinking off, and that a smaller image is faster) were wrong, and only timing
them showed it.
