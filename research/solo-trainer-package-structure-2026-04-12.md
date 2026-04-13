# How Solo Freelance Dog Trainers Structure Their Packages

**Date:** 2026-04-12
**Research Question:** How do independent (solo) dog trainers define and sell training packages — and is a title + description + price form sufficient to build a package feature in Pawgress?
**Decision This Informs:** Package creation feature design and required fields in the Pawgress app.
**Scope:** Solo/independent freelance trainers only. Kennels, daycares, and franchises excluded.

---

### Summary

Solo dog trainers do not sell packages as simple flat-fee offerings. Every package is defined by a specific combination of fields: a name, a session count, a session duration, a delivery format, a total price, and an expiry window. These fields are not optional extras — they are the contractual structure of the package and how both trainer and client track progress and accountability. A title + description + price form alone would leave out the two most critical fields: **session count** (what the client bought and how many remain) and **expiry** (the self-protective deadline trainers almost universally enforce). For Pawgress, a minimal but complete package creation form needs at least five fields, not three.

---

### Key Insights

- **Session count is the core mechanic of every package.** Without it, a "package" is just a label. Trainers define packages by number of sessions: 4, 5, 6, 8, 10, 16 are the most common counts observed across real solo trainer websites. Session count is how a trainer tracks consumption (e.g., "client has 3 of 6 sessions left") and how clients feel the progress of the commitment they paid for. This is the single most important missing field from a title + price + description form.

- **Session duration is always specified — it's part of the contract.** Real packages consistently define session length: 45 min, 60 min, 75 min, 90 min. Duration affects how trainers price their time and sets client expectations. It is not something trainers leave vague. Example from Shelby Semel: "45–60 min sessions" for Fast Track programs. Example from PawsitivePackLeader: "16 × 90-minute sessions" for their intensive coaching package. Duration is standard metadata on every real package observed.

- **Delivery format is a distinct package dimension that affects price and logistics.** Solo trainers consistently differentiate packages by type: in-home, facility/drop-off, and virtual. These are not interchangeable — they carry different price points, travel considerations, and logistical requirements. In-home packages include travel fees. Virtual packages have separate pricing tiers. Trainers don't mix these into one package without specifying. For Pawgress, this matters when a trainer has both in-home and virtual offerings — they need to distinguish them clearly.

- **Expiry windows are nearly universal — trainers enforce them to protect cash flow and compliance.** Across every solo trainer site researched, unused sessions expire on a defined schedule:
  - Standard follow-up packs: 6 months from purchase
  - Intensive Fast Track programs: 2–3 weeks from start
  - Home School 5-pack: 30 days from first session
  - Home School 10-pack: 75 days from first session
  - Separation anxiety programs: 3 months
  Expiry is not bureaucratic — it protects the trainer from holding sessions open indefinitely and motivates owner compliance. This is a field Pawgress should support, even if optional.

- **Packages are customized, not templated — trainers need flexibility, not rigidity.** The Dog Biz Success methodology explicitly coaches solo trainers to recommend custom package sizes per client after an initial consult, rather than selling pre-set tiers. This means trainers need a form they can fill out fluidly for each client relationship, not a rigid dropdown menu. A flexible form (title, session count, duration, type, price, expiry, notes) is the right design over a preset "pick a tier" UI.

- **Add-ons and inclusions are part of how trainers differentiate.** Beyond the core session structure, solo trainers consistently include extras as part of their package value: video recaps after sessions, written training plans, email/text support between sessions, and homework assignments. These are currently described in a "what's included" notes field. Pawgress already handles homework and session summaries natively — this means Pawgress's features ARE the differentiator trainers are manually writing into their package descriptions. This should be surfaced in marketing.

- **Frequency (sessions per week) is often part of the package definition.** Intensive packages specify cadence: "twice weekly" for 16-session programs, "once weekly" for 8-session programs. This is not always a required field but is worth supporting as an optional field so trainers can set client expectations up front.

---

### Recommendations

1. **The minimum viable package form needs 5 fields, not 3.** Title + description + price is insufficient. The required set is:
   - **Title** (e.g., "Reactive Dog Program")
   - **Number of sessions** (e.g., 6) — *the most critical field*
   - **Session duration** (e.g., 60 min)
   - **Total price** (e.g., $850)
   - **Description / what's included** (free text)
   And strongly recommended optional fields:
   - **Session type** (in-home / virtual / facility)
   - **Expiry window** (e.g., sessions must be used within 6 months)
   - **Session frequency** (e.g., once per week)

2. **Build session tracking as the core package mechanic.** Once a package is created and assigned to a client, Pawgress should automatically track sessions used vs. sessions remaining (e.g., "4 of 6 sessions completed"). This is the clearest daily-use value a package feature delivers — trainers and clients can see exactly where they are in the commitment at any time.

3. **Make expiry optional but visible.** Not all packages need expiry, but most do. A simple optional date field ("Sessions expire on: ___") or duration selector ("Sessions expire after: [30 days / 3 months / 6 months / custom]") covers the real-world need without overcomplicating the form.

4. **Do not force pre-set package tiers.** Solo trainers customize packages per client. The UI should feel like filling out a clean form for each new client relationship, not selecting from a menu. Flexibility is the right call for this audience.

5. **Use Pawgress's native features as package selling points in marketing.** Trainers currently write "includes written training plan, homework, and email check-ins" into their package descriptions manually. Pawgress delivers all of that natively (session summaries, homework, notes). Instagram content should frame this: "Your packages already come with everything built in — session summaries, homework tracking, progress notes. You don't have to write it out. Pawgress handles it."

---

### Package Field Reference (What Real Solo Trainers Use)

| Field | Required? | Real-World Examples |
|---|---|---|
| Package name/title | Yes | "Fast Track Puppy," "Reactive Dog Program," "Package B," "Home School" |
| Number of sessions | Yes | 4, 5, 6, 8, 10, 16, 22 |
| Session duration | Yes | 45 min, 60 min, 75 min, 90 min |
| Session type | Yes | In-home, virtual, facility/drop-off |
| Total price | Yes | $525 – $3,200 |
| Description / what's included | Yes | Free text: goals, behaviors, extras |
| Expiry window | Strongly recommended | 30 days, 75 days, 3 months, 6 months |
| Session frequency | Optional | Once/week, twice/week |
| Add-ons / travel fee | Optional | Extra dog (+$50), travel fee (+$35) |
| Per-session value | Optional (auto-calc) | Shown to client as value signal |

---

### Data Sources

- [How to Sell Dog Training Packages — Dog Biz Success](https://dogbizsuccess.com/get-the-right-clients-part-3-selling-the-training-package/)
- [Private Sessions & Package Structure — Shelby Semel Dog Training](https://www.shelbydogtraining.com/private-sessions)
- [Coaching Packages — PawsitivePackLeader](https://pawsitivepackleader.com/private-dog-training/)
- [Private Training Packages — Thumbtack Price Guide](https://www.thumbtack.com/p/private-dog-training-prices)
- [PT Session Expiry Dates — Fitpro Income](https://fitproincome.com/personal-training-sessions-expiry-date/)
- [Dog Training Prices 2026 — Bark](https://www.bark.com/en/us/dog-training/dog-trainer-prices/)
- [Setting Up a Profitable Dog Training Business — Gingr](https://www.gingrapp.com/blog/setting-up-a-profitable-dog-training-business)
