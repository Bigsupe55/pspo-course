# COURSE SPEC

The authoring contract. Every agent that wrote a module read this first. It exists so that fourteen modules written in parallel by seven different authors read as one voice and validate against one schema.

This file is checked in because it is the actual mechanism, not documentation written afterwards.

---

## 1. THE LEARNER

Everything below follows from one paragraph. Write to this person, not to a general audience.

A **founder acting as Product Owner** while also carrying strategy, sales, and marketing. **Starting cold on Scrum**: never assume a term is known, and define any Scrum term in the same breath as its first use. Their team includes a couple of certified Scrum Masters who wear other hats, so there is real expertise to lean on rather than override.

Their stated goal, in their words: *"I really want to hone in on what a PO does, how they do it, why they do what they do."* **The WHY is the priority.** Never state a rule without the reasoning behind it.

Target: pass **PSPO I** in four to six weeks, then eventually **CSPO**.

They get bored by walls of text. That is a design constraint, not a preference.

### HARD RULES

1. **No em dashes.** Commas, colons, parentheses, or a full stop.
2. **No timers, countdowns, or time pressure anywhere.** The learner rejected timed practice. The real exam is timed; this course deliberately is not. Naming an event's official timebox is correct. Writing copy that implies a clock the learner is racing is not.
3. **No beat body over 130 words.** Longer means split it.
4. **Second person.** Warm, direct, a little dry. Never corporate-cheerful, never condescending.
5. **Accuracy over everything.** The Scrum Guide 2020 is the sole authority for what Scrum IS.

---

## 2. CONTENT SCHEMA

One JSON file per module. Must parse with `JSON.parse`.

```jsonc
{
  "id": "m01", "num": 1, "week": 1,
  "title": "...", "subtitle": "One sentence, plain language, no jargon.",
  "minutes": 25,
  "why": "One sentence: why a Product Owner who skips this gets burned.",
  "objectives": ["3 to 5 outcome statements, each starting with a verb"],
  "beats": [ /* below */ ],
  "quiz":  [ /* 8 to 12 questions */ ],
  "cards": [ /* 8 to 12 flashcards */ ]
}
```

### Beat types

Open with `hook`, close with `keypoints`, and never place two `teach` beats back to back without something interactive or visual between them.

```jsonc
{"type":"hook",     "body":"2 to 4 sentences that make the module feel necessary."}
{"type":"analogy",  "title":"...", "body":"A plain-world metaphor.", "visual":"optional-key"}
{"type":"teach",    "title":"...", "body":"Markdown-lite.", "callout":{"kind":"note|warn|why","text":"..."}}
{"type":"guide",    "quote":"VERBATIM Scrum Guide 2020 text.", "cite":"Section", "gloss":"Plain English."}
{"type":"trap",     "myth":"What people wrongly believe.", "truth":"What the Guide says.", "why":"Why the exam asks."}
{"type":"civic",    "title":"...", "body":"Applies the concept to the running product scenario."}
{"type":"check",    "q":{ /* a question object */ }}
{"type":"sim",      "title":"...", "setup":"...", "choices":[{"label","outcome","verdict":"good|mixed|bad","lesson"}]}
{"type":"write",    "prompt":"...", "rubric":["3 to 5 criteria"], "model":"A strong example answer."}
{"type":"keypoints","points":["3 to 5 one-line takeaways"]}
```

`visual` keys the engine draws: `empirical-loop`, `scrum-machine`, `backlog-funnel`, `sprint-timeline`, `value-quadrants`, `stakeholder-map`, `ordering-matrix`, `dod-gate`, `goal-nesting`.

### Question schema

```jsonc
{
  "id": "m01q1",
  "kind": "mcq",          // mcq | multi | tf | order | sort
  "stem": "Situational, not trivia.",
  "options": ["A","B","C","D"],
  "answer": 2,            // mcq: index | multi: [indices] | tf: boolean
  "explain": "Why the key is right AND why each tempting wrong answer is wrong.",
  "cite": "Scrum Guide 2020, section name",
  "tag": "accountabilities|events|artifacts|value|backlog|stakeholders|empiricism|antipatterns"
}
```

`order` adds `items` in correct order (the engine shuffles). `sort` adds `buckets` and `items` of `{text, bucket}`. `multi` stems must state how many to pick.

---

## 3. THE FIDELITY RULE

This is the rule that makes the course worth more than a generic one.

PSPO I is graded against the Scrum Guide 2020, strictly. Adjacent training material teaches useful practices that are **not Scrum**. Confusing the two is the most common way people fail.

So anything taught that is NOT in the Scrum Guide 2020 carries this inline marker at the start of the relevant sentence:

```
[[PRACTICE]]
```

The engine renders it as a visible "Practice, not Scrum" badge.

**Requires the marker:** user stories, story points, velocity, personas, Definition of Ready, MoSCoW, planning poker, the three questions in the Daily Scrum, backlog grooming, release planning, Sprint 0, epics, INVEST, the PO "accepting" stories, and all of Evidence-Based Management (official Scrum.org material, but not the Guide).

**Must be stated precisely, because the exam tests the wording:**

- The Product Owner is **accountable for maximizing the value of the product resulting from the work of the Scrum Team**.
- Product Backlog management is exactly four bullets: developing and explicitly communicating the Product Goal; creating and clearly communicating Product Backlog items; ordering Product Backlog items; ensuring the Product Backlog is transparent, visible and understood.
- The PO **may delegate** the work but **remains accountable**.
- The Product Owner is **one person, not a committee**.
- **Only the Product Owner has the authority to cancel a Sprint.**
- **The Developers who will be doing the work are responsible for the sizing.**
- The Sprint Goal is a **commitment by the Developers**, crafted by the whole Scrum Team, **finalized before Sprint Planning ends**.
- The Daily Scrum is **for the Developers**. The PO attends only **as a Developer**, and only if actively working on Sprint Backlog items.
- Timeboxes for a one-month Sprint: Planning **8h**, Review **4h**, Retrospective **3h**, Daily Scrum **15 min**.
- The Sprint Review is the **second to last event** and is a working session, not a presentation.
- Refinement is an **ongoing activity**, not an event.
- The Product Goal is **in the Product Backlog**; the team must **fulfill or abandon** one before taking the next.
- An Increment **may be delivered before the Sprint ends**. The Sprint Review is **never a gate to releasing value**.
- Scrum is founded on **empiricism and lean thinking**. Pillars: **transparency, inspection, adaptation**. Values: **Commitment, Focus, Openness, Respect, Courage**.
- The framework is **purposefully incomplete**.

---

## 4. TONE CALIBRATION

Bad, because it is abstract, long, and says nothing a reader could not guess:

> The Product Owner is a critical role within the Scrum framework who is responsible for maximizing the value delivered by the Development Team through effective management of the Product Backlog and continuous stakeholder engagement across the organization.

Good, because it commits to a claim and gets to the why:

> You own one question: of everything we could build next, what is worth building next? That is the whole job. Everything else, the meetings, the writing, the saying no, exists to make your answer to that question a good one.

Analogies come from ordinary life, not from software. A restaurant kitchen, a road trip, a poker hand, a budget hearing. Avoid the tired ones: no orchestra conductor, no building a car.

---

## 5. VALIDATION

Nothing is reported as done until it parses and passes. See [docs/verification.md](docs/verification.md) for what the build enforces.
