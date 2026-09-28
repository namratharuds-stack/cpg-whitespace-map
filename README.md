# CPG Commercial Execution: Whitespace Map

Twelve problems in CPG sales execution, revenue growth management, B2B commerce, and commercial contracts that no current tool solves end to end.

Each entry covers:
- the gap
- the tools that come closest
- why the gap is **architectural rather than accidental**
- what solving it could look like

I wrote this after 7.5 years building sales-execution, RGM, and B2B commerce products for CPG. Several entries became [FieldIQ](https://fieldiq-pro-pilot.lovable.app) features.

**Pattern across all twelve:** the data usually exists. It sits in two systems bought by two different buyers, and nobody owns the step between them. CLM stops at the commercial manager, SFA stops at the SKU, and feedback tools stop at the NPS score.

---

## At a glance

| # | Gap | Domain | Closest tools today | Status |
|---|---|---|---|---|
| 1.1 | Contract obligations at rep level | Sales execution | Vistex, Icertis · BeatRoute, FieldAssist | **Built:** [CommCheck](https://github.com/namratharuds-stack/fieldiq-product-specs) |
| 1.2 | New outlet onboarding visibility | Sales execution | SFA + ERP + CLM, unconnected | **Prototyped:** OnboardIQ, rules-based |
| 1.3 | Competitor activity synthesis | Sales execution | Wiser, Repsly | **Partial:** Territory Pulse |
| 1.4 | Post-visit quality scoring | Sales execution | Ivy Mobility AI Sales Coach, BeatRoute Copilot | Open |
| 2.1 | Promo post-mortem in 48 hours | RGM | o9, Vistex, SAP TPM | Open (PRD written) |
| 2.2 | Trade spend anomaly explainer | RGM | Vistex, SAP TPM | Open |
| 2.3 | SKU rationalization impact by outlet | RGM | o9, NielsenIQ | Open |
| 3.1 | Distributor loyalty tier-drop prediction | B2B commerce | Salesforce Commerce Cloud | Open |
| 3.2 | B2B portal adoption friction | B2B commerce | Salesforce Commerce Cloud, CustomerGauge | Open |
| 3.3 | Distributor NPS → commercial action | B2B commerce | CustomerGauge, Salesforce CRM | Open |
| 4.1 | Forward-looking contract breach risk | Contracts | Vistex, Icertis, Conga | Open (PRD written) |
| 4.2 | Deduction dispute decision support | Contracts | Vistex, HighRadius | Open |

---

## Domain 1: Sales execution and route to market

### 1.1 Contract obligations at rep level
**Gap:** Volume commitments, co-op deadlines, and payment breaches never reach the field rep before a visit. They live in CLM systems only HQ can open.
**Closest:** Vistex and Icertis handle CLM for commercial teams. BeatRoute and FieldAssist are SFA tools for reps. Neither connects to the other.
**Why it's open:** CLM and SFA were built for different buyers and were never designed to connect at the field layer.
**Status:** Built as **CommCheck**, a pre-visit briefing that sorts each outlet into *Act Today*, *Opportunity*, or *Escalate*.

### 1.2 New outlet onboarding visibility
**Gap:** Onboarding a new outlet means a credit check, contract setup, catalog access, and loyalty enrollment across three or four systems. The rep can't see any of it and learns the status by calling the office.
**Closest:** SFA captures the lead, ERP handles credit, and CLM handles the contract. Nothing shows where the outlet is in the overall journey.
**Why it's open:** Each tool owns one step, and nobody owns the handoffs between them.
**Status:** Prototyped as **OnboardIQ** in FieldIQ, deliberately **rules-based with no LLM**. The problem is a four-stage state machine with fixed thresholds, and a model would only add latency and non-determinism to arithmetic.

### 1.3 Competitor activity synthesis
**Gap:** Reps log competitor activity in a form field every day. Nobody aggregates those observations into a territory-level signal a sales manager can act on.
**Closest:** Wiser (crowdsourced shelf data) and Repsly (manual competitor logging).
**Why it's open:** Competitor data is treated as a form field, not a signal. The layer that turns 200 observations into "Competitor X is pushing hard in the northeast this week" doesn't exist.
**What solving it looks like:** A manager picks a territory and a period. The tool returns the top competitor moves, the outlets most exposed, and a response for each tier.
**Status:** Partly addressed by **Territory Pulse**, which synthesizes across outlets for a single rep. Aggregation across reps is still open.

### 1.4 Post-visit quality scoring
**Gap:** SFA records that 18 visits happened, not whether the rep had the right conversation, addressed the commercial issue, or activated the promo.
**Closest:** Ivy Mobility's AI Sales Coach gives in-visit guidance. BeatRoute Copilot gives manager analytics.
**Why it's open:** Scoring quality means comparing what the rep entered with what was expected at that outlet (contract targets, promo requirements, open issues), and no tool does that synthesis.
**What solving it looks like:** A visit score against the outlet's known obligations, with the specific missed opportunities, plus a weekly quality-versus-quantity digest for the manager.

---

## Domain 2: Revenue growth management

### 2.1 Promo post-mortem in 48 hours
**Gap:** Post-promo analysis takes weeks because the data lives in four systems. By the time it's ready, the next promo is already set.
**Closest:** o9 (planning) and Vistex / SAP TPM (trade promotion management). Both produce retrospective analytics that need an analyst to assemble.
**Why it's open:** The data exists but is never assembled fast enough to influence the next decision.
**What solving it looks like:** From the promo parameters, a structured post-mortem within 48 hours of close: estimated uplift against baseline, likely compliance issues, a root-cause hypothesis, and a recommendation for the next event.

### 2.2 Trade spend anomaly explainer
**Gap:** Finance finds trade spend variances at month close, then spends days reconciling ERP, TPM, and CLM to explain them.
**Closest:** Vistex (deduction management) and SAP TPM (accruals). Both surface the anomaly, and neither explains it.
**Why it's open:** The explanation needs data from several systems, and no single tool owns all of it.
**What solving it looks like:** The most likely root cause from five categories (contract terms, promo compliance, deduction dispute, accrual error, volume mix), the reasoning behind it, and the next step.

### 2.3 SKU rationalization impact by outlet
**Gap:** Finance proposes delisting a SKU and the field pushes back, because some outlets depend on it. Nobody can quickly show which outlets and how much revenue are at stake.
**Closest:** o9 (assortment planning at the aggregate level) and NielsenIQ (category data).
**Why it's open:** Outlet-level SKU dependency lives in SFA and DMS, while assortment planning works at the aggregate level. Nobody connects the two.
**What solving it looks like:**
- which outlets carry the SKU
- revenue at risk by tier
- outlets where it's their only product in the category
- a replacement SKU to offer each affected outlet

---

## Domain 3: B2B commerce and loyalty

### 3.1 Distributor loyalty tier-drop prediction
**Gap:** Commercial teams learn a distributor is dropping a loyalty tier at quarter close, after the window to intervene has passed.
**Closest:** Salesforce Commerce Cloud and B2B loyalty portals show the current tier, not the trajectory.
**Why it's open:** Prediction means combining purchase trajectory, tier thresholds, and weeks remaining. No loyalty tool does this for distributors.
**What solving it looks like:** A tier-drop probability, the volume gap to hold the tier, a recommended intervention, and how urgent it is.

### 3.2 B2B portal adoption friction
**Gap:** Months after launch, many distributors still order by phone or email. Analytics show who isn't adopting, not why.
**Closest:** Salesforce Commerce Cloud (usage) and CustomerGauge (NPS).
**Why it's open:** Adoption gets treated as a training problem rather than a product design problem, so nobody builds the diagnostic layer.
**What solving it looks like:** A root-cause hypothesis for each segment (UX friction, trust gap, capability gap, workflow mismatch, or change resistance) and an intervention sized to each group.

### 3.3 Distributor NPS → commercial action
**Gap:** A distributor scores you 4/10 and writes "claims take three weeks and nobody calls back." The rep visits on Thursday without knowing.
**Closest:** CustomerGauge (feedback) and Salesforce CRM (commercial records). They don't connect.
**Why it's open:** Feedback systems and execution systems are separate purchases, and neither vendor owns both sides.
**What solving it looks like:** A categorized root cause, an urgency score, the action for the rep before the next visit, and an escalation flag below a set score.

---

## Domain 4: Contracts and commercial terms

### 4.1 Forward-looking contract breach risk
**Gap:** Nobody watches distributor contract obligations against actual performance during the quarter. Breaches show up at close.
**Closest:** Vistex, Icertis, and Conga track the obligations but don't forecast breaches.
**Why it's open:** Predicting obligation risk means combining contract terms from CLM with performance to date from ERP/DMS, and no CLM vendor has turned that into a product.
**What solving it looks like:** A breach probability, the obligation most at risk, the weeks left to intervene, and the commercial conversation to have now.

### 4.2 Deduction dispute decision support
**Gap:** A distributor files a deduction claiming the promo wasn't executed. The commercial manager has days to respond and spends most of them gathering data.
**Closest:** Vistex (deduction workflows) and HighRadius (AR automation). Both process deductions, and neither helps decide whether to dispute.
**Why it's open:** Deciding needs contract terms, shipment data, and promo compliance together.
**What solving it looks like:** A validity call (likely valid, disputed, or insufficient data), the reasoning, the data needed to confirm it, and draft response language.

---

## Related

- [FieldIQ live demo](https://fieldiq-pro-pilot.lovable.app)
- [FieldIQ product specs](https://github.com/namratharuds-stack/fieldiq-product-specs): PRD and agent specs for the built entries
- [FieldIQ evals](https://github.com/namratharuds-stack/fieldiq-evals): how the built agents are tested

Tool descriptions reflect public positioning as of mid-2026 and may have changed.

---

[Namratha Rudrappa](https://namratharudrappa.com) · Senior PM, Applied AI for CPG commercial execution
