# The Northfield world

**This file is the transformation contract.** The course was originally written against a real company's internal material. This public version replaces all of that with one consistent fictional world. Every agent rewriting content must use this file as the single source of truth so that all 14 modules describe the same town, the same product, and the same people.

---

## 1. THE HARD RULE

**Nothing real about the original company may survive.** Not a name, not a number, not a compliance status, not a pricing threshold, not a roadmap item id, not a strategic tension.

These strings must appear **zero** times in the finished content. The build fails if any of them do:

```
Civic-Chain, CivicChain, Tyler Munis, Munis, Levesque, Ouellette, Thibodeau,
Okafor, Gagnon, Baltimore, Open Checkbook, Board of Estimates, Topsham,
NOW-1..NOW-9, NEXT-1..NEXT-12, LATER-1..LATER-12, FOAA, MMA, 30-A, 5603,
Anomaly Center, Query Terminal, Harbor and Waterfront
```

Also avoid naming a real US state, a real municipality, or a real ERP vendor anywhere in the applied scenarios.

**What you KEEP, untouched:** every word of Scrum teaching. All `guide` beat quotes stay verbatim from the Scrum Guide 2020. All `trap` beats keep their exact myth/truth. Every quiz answer index, explanation, and citation stays correct. You are re-skinning the applied examples, not re-teaching Scrum.

---

## 2. THE SETTING

**Northfield** is a fictional New England town of about 5,200 residents. It runs on a July-to-June fiscal year. Its Select Board of five part-time members meets twice a month. It is not in any named state; say "state law" rather than citing a statute, and never invent a statute number.

**Ledgerline** is the product. A municipal budget transparency and spend-monitoring platform sold to small towns. You are its Product Owner at a young govtech company. The company is never named.

**Corvus Financials** is the fictional ERP most towns already run. Ledgerline reads from it on a nightly feed.

### The screens that exist
| Screen | What it does |
|---|---|
| **Budget Pace** | Per-department spend against appropriation, with pace flags |
| **Executive Overview** | The one-page roll-up a Town Manager reads |
| **Anomaly Review** | Flags unusual transactions for triage |
| **Ask the Ledger** | Natural-language question box that returns a table plus the query it ran |
| **Data Connections** | Feed health for the Corvus sync and the bank file |
| **Vendor Register** | Every vendor and what they were paid |
| **Records Desk** | Produces a dated, provenance-stamped public-records response |

### Roadmap ids
Use `R-01` through `R-24`. Never the original scheme.

### Money and thresholds (invented Northfield policy)
- Over **$25,000**: formal RFP plus a Select Board vote
- **$7,500 to $25,000**: three written quotes
- Under **$7,500**: the Town Manager can sign alone
- A Ledgerline pilot is priced at **$4,800/year**, deliberately under that last line

---

## 3. THE PEOPLE

Use these names consistently. They replace the original personas one-for-one in role, never in name.

| Name | Role | Wants | Fears |
|---|---|---|---|
| **Dana Whitcomb** | Finance Director | To stop finding surprises in month-end close | Being blamed for a number she did not know was wrong |
| **Priya Raman** | Treasurer | To sign the payment warrant without personal risk | Her signature on a disbursement that does not reconcile |
| **Glen Ostrowski** | Purchasing Officer | Contracts followed and thresholds respected | An audit finding on a bid he waived |
| **Yusuf Adeyemi, CPA** | External auditor | A defensible sample and a clean trail | Evidence he cannot reproduce next year |
| **Carla Benitez** | IT coordinator, shared across three towns | Nothing new to maintain | Becoming the support desk for a vendor's product |
| **Margaret Shaw** | Town Clerk | To answer records requests without losing a day | Handing a resident something wrong or over-disclosed |
| **Tom Iverson** | Town Manager | A budget conversation that is not a fight | Looking uninformed in a public meeting |
| **Ruth Delgado** | Select Board chair | To vote on things she understands | Approving something she will be asked about later |
| **Angela Pike** | Accounts Payable clerk | Fewer keystrokes, fewer callbacks | Being the last person to touch a bad payment |
| **A resident** | Beneficiary | To see where the money went | Being fobbed off |

**Buyer vs user vs beneficiary:** Tom Iverson and the Select Board sign. Dana, Angela, Priya, Glen and Margaret use it daily. Residents and Yusuf benefit but rarely log in. That split is the whole lesson in the stakeholder module.

---

## 4. THE SCENARIO ARCHETYPES

These are the teaching situations. They are ordinary product-management problems, which is why they work. Re-specify them in Northfield terms wherever the original used a real company situation.

1. **The flag you cannot clear.** Dana loves Anomaly Review and immediately distrusts it: she cannot see the rule behind a flag or dismiss a false positive. Angela works that screen daily and can only look. One engineer available.
2. **The feed that died quietly.** The Corvus sync sat in Error for two days, zero records, visible only if you opened Data Connections. Every budget number on every screen was silently stale. Filed low priority while a higher-priority feature depended on it.
3. **Two screens, two answers, one meeting.** Budget Pace says four departments are over pace, Executive Overview says three. One rounds before filtering, the other after. A department sitting at 1.905 percent lands on either side. The board packet is printed from one of them.
4. **The band that could never fire.** A gold "Watch" state was unreachable: it was measured on a year-end utilisation band while "At risk" used a projection, and at 75 percent elapsed the at-risk rule always claimed the row first. Dead code under a live-looking legend.
5. **The tool nobody agrees on.** Yusuf calls Ask the Ledger the most valuable thing built. Dana would trade it for reliable saved views. Margaret fears a resident reading over her shoulder. Ruth will never open it. Cutting it is on the table.
6. **The differentiator nobody logs in for.** Discovery concludes operators trust the product because of reconciliation and clear definitions, not because of the technology the company leads with in its pitch.
7. **The adoption gate you cannot fake.** Everything on the roadmap ships except the one thing Priya says determines whether she can use the product at all: a tie-out between Corvus, the bank file, and the ledger. It needs a real backend months away.
8. **The town that already solved it.** A larger prospect already publishes its own spend data and is proud of it. Transparency cannot be the pitch there; the opening has to be re-derived for that segment.
9. **The threshold line.** Pricing is set under the Town Manager's unilateral signing authority specifically so a pilot never needs a board vote. A procedural constraint, not a commercial one.
10. **The certification demanded mid-deal.** An IT director makes SOC 2 a requirement. Controls are implemented, the audit is not scheduled, and accessibility has never been formally assessed. What may a Product Owner commit to?
11. **The approval you may not route around.** State law says the treasurer may disburse only on a warrant the Select Board has voted and signed. Boards meet twice monthly. Any faster-payment feature must live inside that workflow, not beside it.
12. **The demo clock.** The sample data is 75 percent consumed against a July-to-June year, which pins it to a fixed date. Switching to the live clock makes the town look like it spent 75 percent of its budget in six weeks and breaks every projection on screen. You can have any two of three properties.
13. **One human, several hats.** Ten clean personas, but in a town this size the same person is often Finance Director and Treasurer, and the Clerk also runs payroll. Role separation should drive permissions without forcing a second login.
14. **The seats that did not make the welcome screen.** Onboarding offers five roles. Accounts Payable and IT are cut, with the written reason that neither signs a contract, even though Angela's daily work changes most.
15. **The table that must not sort.** Sorting shipped across seventeen tables and six were deliberately excluded: sorting query results would make the printed query above them a lie, the auditor's sample order IS the sampling method, and the board packet and records letter are frozen documents whose prose says "listed below."
16. **Value for someone who is not the buyer.** Margaret wants the Records Desk. Records requests average a few a month, the deep ones eat more than five hours, and most are really about vendor payments. The buyer feels none of that pain.

---

## 5. HOW TO REWRITE

For each module JSON:

1. Read every string. Where it names the original company, its people, its vendors, its roadmap ids, its compliance status, its markets, or its strategy, **rewrite it into Northfield**.
2. Keep the *pedagogical shape* identical. If a sim had four choices with verdicts good/mixed/mixed/bad, it still does, testing the same principle.
3. Keep every `guide` quote **byte-identical**. Keep every `trap` myth and truth identical. Keep every quiz `answer`, `explain`, and `cite` correct; you may reword a stem's setting, never its Scrum logic.
4. Do not change `id`, `num`, `week`, `minutes`, `kind`, `answer`, `tag`, or any `visual` key.
5. The attribution line anywhere origin is mentioned is: **"built while founding a govtech startup."** Never name the company.

### The rules that still apply
- **No em dashes.** Anywhere. Commas, colons, parentheses.
- **No timers, countdowns, or pacing language.** The learner rejected them.
- No beat body over 130 words.
- `[[PRACTICE]]` stays on anything not in the Scrum Guide 2020.
