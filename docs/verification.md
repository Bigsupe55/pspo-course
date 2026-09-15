# Verification

The failure mode for generated course content is not that it looks wrong. It is that it looks right and teaches something false. A certification course amplifies that: a confident wrong answer gets memorised.

So the build refuses to ship content it cannot check. `python build.py` runs every check below and exits non-zero on failure.

---

## 1. Structural integrity

Content is JSON, so most classes of error are mechanically detectable:

| Check | Why it exists |
|---|---|
| Every `mcq` answer index is within its `options` array | An off-by-one makes a correct answer unreachable and silently marks the learner wrong |
| Every `multi` answer is a list, in range, non-empty | Same, and a scalar here would throw at grade time |
| Every `tf` answer is a real boolean | `"true"` as a string grades every answer wrong |
| Every `sort` item's bucket exists in that question's `buckets` | An orphan bucket makes the question unanswerable |
| No duplicate question ids, anywhere, including across exams | Ids key the progress store, so a collision corrupts saved results |
| No duplicate flashcard ids | Ids key the spaced-repetition schedule |
| Every question has a non-empty explanation | An unexplained wrong answer teaches nothing |

## 2. Content invariants

Two rules came from the learner and are enforced rather than trusted:

- **Zero em dashes and en dashes** in shipped content.
- **Zero timer, countdown, or pacing language.** The learner rejected timed practice. The real exam is timed; the course deliberately is not, and no copy implies otherwise. Naming an event's official timebox is correct and expected; talking about a clock the learner is racing is not.

## 3. The sanitization tripwire

This repo is public. The course was originally written against a private company's internal material, and that material was replaced with a fictional town (see [`WORLD.md`](../WORLD.md)).

The build scans the **finished page**, not the source files, for a list of banned strings: company name, people, vendors, markets, roadmap identifiers, compliance specifics. If any survive, the build:

1. prints every hit with a count,
2. **deletes the output file**, so a leaking build cannot be served by accident,
3. exits non-zero.

Scanning the built artifact rather than the sources is the point. Content can reach the page through several routes, including CSS comments, which do ship. The only scan that proves anything is the one on what actually gets published.

## 4. Source fidelity

PSPO I is graded against the Scrum Guide 2020, so quoting it loosely is a correctness bug, not a style one.

- Every `guide` beat quote is **copy-pasted from the Guide's text**, not paraphrased, and was confirmed by substring match against the source.
- Claims of absence are grepped. The course states that several widely-assumed terms never appear in the Guide. Verified against the source text:

```
story point        0        user story        0        Definition of Ready  0
velocity           0        Sprint 0          0        grooming             0
hardening          0        three questions   0
```

`ready` appears exactly once, lowercase, as a property of an item rather than as a gate. The only occurrence of the `accept` family in the entire Guide is `acceptable`, in an unrelated sentence, which is what makes "the Product Owner accepts stories" checkable as false rather than merely doubted.

## 5. Behaviour

The application was exercised in a real browser, not reasoned about:

- Every question type answered end to end: single choice, multiple answer, true or false, drag-to-order, sort-into-buckets.
- Branching scenarios, exam submission and scoring, flashcard scheduling, and answer persistence across navigation.
- Both themes measured for contrast against WCAG AA. Two real failures were found at 2.8:1 and 2.97:1 and fixed by adding a darker token for text while keeping the lighter one for fills.
- Horizontal overflow checked on every view at 265px wide. One real bug found: a grid with a fixed `minmax(268px, 1fr)` cannot fit a narrower viewport. Fixed with `minmax(min(268px, 100%), 1fr)`.

## 6. What is not verified

Stated plainly, because an honest limits section is worth more than a longer checklist.

- **Scrum correctness of every question was sampled, not exhaustively proven.** Answer keys were checked across every topic against the Guide, and the sample was clean. 317 questions were not individually adjudicated by a certified trainer.
- **The Claude-powered features cannot run in the public demo**, so their behaviour here is the graceful-degradation path only.
- **No automated test suite.** The checks above run at build time; there is no unit test layer, because the application has almost no logic worth unit testing separately from the content it renders.
