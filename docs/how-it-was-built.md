# How it was built

A 14-module course with 317 questions is more writing than one model call, or one agent, can do well. This is how it was actually produced, including the parts that broke.

---

## The shape of the problem

Course content has a property that makes it awkward for language models: it must be **internally consistent across a lot of output**. Module 9 has to use the same vocabulary as module 2. A question in mock exam 1 must not contradict a trap taught in module 13. Fourteen modules written independently by fourteen sessions will drift in voice, repeat each other, and disagree.

The usual fix is to write it all in one long context. That fails differently: quality degrades over a long generation, and one failure loses everything.

So the work was split across parallel authoring agents, with consistency enforced by artifacts rather than by memory.

## Consistency through a written contract

Before any content existed, one file was written: an authoring spec, checked into the repo as [`COURSE-SPEC.md`](../COURSE-SPEC.md).

It fixes the things that would otherwise drift:

- **The learner.** One paragraph describing exactly who this is for. Every agent writes to the same person.
- **The JSON schema.** Ten beat types, a question schema, a flashcard schema. Content is data, not prose, so it can be validated.
- **Voice, with worked examples.** A "bad" sample and a "good" sample, so tone is demonstrated rather than adjectivally described.
- **The accuracy rule.** The Scrum Guide 2020 is the only authority for what Scrum *is*. Anything that is common practice but absent from the Guide carries an inline `[[PRACTICE]]` marker that renders as a visible badge.

Each agent read the spec, then wrote its modules. The spec is the reason seven independent authors produced something that reads as one voice.

## Research separated from authoring

Authoring agents did not read source PDFs. A first wave of research agents did, and each wrote a structured brief to disk. The authoring wave read briefs.

This matters for two reasons. Source material is long and mostly irrelevant to any one module, so briefs cut the context each author needs. And a brief can be checked once, by a human, instead of being re-derived (and re-misread) by every agent that touches it.

## What actually went wrong

**Agents died mid-run, twice**, when the session hit a usage limit. The first time, six agents were in flight and all six were killed.

The fix was not retries. It was changing what "progress" means:

> Write each file to disk the moment it is finished, before starting the next. Never hold more than one unit of work in memory.

After that instruction, a killed agent lost at most one file instead of its whole batch. When the limit hit a second time, 12 of 14 modules had already landed. Recovery was re-running two, not fourteen.

The same principle was applied when a later agent had to produce 80 exam questions: it was told to write them in three separate numbered batches, each a standalone JSON array, merged at build time. A crash costs one batch.

**The lesson is unglamorous and general.** For long agent runs, durability beats cleverness. Design the unit of work so that a crash is cheap, and assume the crash.

## Verification, not vibes

A course that teaches the wrong thing is worse than no course, and a model that is confidently wrong reads exactly like a model that is right. So claims are checked mechanically wherever checking is possible. That is its own document: [verification.md](verification.md).

The single highest-value check: the course asserts in several places that a term "appears zero times in the Scrum Guide." Every one of those claims was verified by grepping the Guide's own text. All held, including the sharpest one, that the word *ready* appears exactly once, lowercase, as a property rather than as a gate.

## What I would do differently

- **Stream the work to disk from the start**, not after the first outage.
- **Pin the content schema in a validator before writing content**, not alongside it. Some early files needed fixing to match the schema they were supposed to follow.
- **Fewer, larger agents.** Seven parallel authors hit the usage ceiling fast. Four would have finished sooner in wall-clock terms because nothing would have been re-run.

## The stack

No framework. Python assembles JSON content and hand-written CSS and JavaScript into one self-contained HTML file. No build step beyond `python build.py`, no dependencies, no bundler. The whole application is about 2,000 lines, and the content is about 700KB of JSON.

That choice was deliberate: the interesting engineering here is the content pipeline and its guarantees, not the frontend toolchain.
