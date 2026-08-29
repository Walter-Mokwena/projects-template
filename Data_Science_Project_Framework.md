# The Data Science Project Playbook
### A repeatable, documented framework for every analysis or data science project

This is your standing operating procedure. Every time you start a new project (telco churn, retail insights, whatever comes next), you copy this template into a new project log and fill it in **as you go, not after the fact**. The goal isn't just to do the analysis — it's to leave a paper trail of *why* you made each decision, so anyone reading it (a recruiter, a client, future-you) can follow your reasoning.

It's built from the frameworks you've been studying: BCG X's 5-step methodology, Microsoft's Prepare→Model→Visualize→Analyze→Manage cycle, the SCAN framework for EDA, and Tata's business-scenario framing. I've stitched them into one continuous pipeline.

---

## Project Brief (the abstract — write this last, place it first)

Every finished project gets a one-page brief pinned to the top of the log, above Stage 1. Think of it as the abstract of a paper: someone should be able to read only this and understand the whole project in under a minute. You write it *last*, once everything else is done, but it's the first thing anyone reads — including you, six months from now, trying to remember what you did.

**Template:**
```
# [Project Title]

**One-line summary:** (the business question and the headline answer, in a single sentence)

**Context:** (2–3 sentences — who the client/stakeholder is, why this mattered now)

**Approach:** (2–3 sentences — data used, method/model, and why that method fit the problem)

**Key finding(s):** (2–3 bullet points — the results that matter)

**Recommendation:** (1–2 sentences — the action this leads to)

**Tools & methods:** (e.g., Python/Pandas, Random Forest, SQL, Power BI)

**Status/scope:** (complete / in progress — and what's explicitly out of scope)
```

**Telco example:**
```
# Telco Customer Churn: Drivers and Retention Targeting

**One-line summary:** Month-to-month customers with no add-on services churn at nearly
3x the rate of annual-contract customers with add-ons — retention offers should target
this segment first.

**Context:** An online telco wanted to understand what drives churn ahead of contract
renewal season, so the retention team could prioritize outreach.

**Approach:** Analyzed a customer-level dataset (~7,000 records) combining contract,
billing, and service-usage data; engineered tenure and service-count features; trained
a Random Forest classifier to rank churn risk and surface key drivers.

**Key findings:**
- Contract type is the single strongest churn predictor
- Lack of tech support/add-ons compounds risk independent of contract type
- Risk drops sharply after 24 months tenure

**Recommendation:** Target month-to-month, no-add-on customers with a bundled
retention offer 60 days before renewal.

**Tools & methods:** Python (Pandas, scikit-learn), SQL for extraction, SCAN framework for EDA.

**Status/scope:** Complete. Does not include a cost-benefit model for the retention
offer itself — flagged as a next step.
```

---

## 0. How to Document (do this for every stage, every project)

Keep one running file per project — call it `project-log.md`. For **every stage below**, log four things before you move on:

```
### [Stage name] — [date]
**What I did:** (the concrete action — queries run, columns dropped, model trained)
**Why:** (the reasoning — what question this answers, what you were testing)
**What I found / decided:** (the result, and the decision it led to)
**What I'd reconsider if new info came in:** (your assumptions, flagged honestly)
```

This is what turns a notebook into a case study. It's also what you present in Stage 9 (Insights & Recommendations) — you're not writing that section from scratch, you're compiling the log.

---

## 1. Business Understanding & Problem Framing

**Purpose:** Before touching data, understand *why this project exists*. BCG X calls this the anchor step — everything downstream is judged against whether it serves this problem.

**Guiding questions to answer in writing:**
- What business decision is this analysis meant to inform?
- Who asked for this, and what do they actually need to *decide* or *do* differently afterward?
- What does success look like — a number, a recommendation, a go/no-go?
- What's the cost of getting this wrong (false positive vs false negative, in business terms)?

**Steps:**
1. Restate the brief in one sentence: "The business wants to know X so they can decide Y."
2. List what you *don't* know yet that you need to ask or assume.
3. Write down 2–3 explicit assumptions you're making about scope, and flag them as assumptions (not facts).

**Document:**
```
**Business problem (1 sentence):**
**Decision this analysis informs:**
**Success criteria:**
**Assumptions made (and why):**
```

**Telco example:** "The business wants to know which customers are likely to churn and why, so retention/marketing can target interventions before contract renewal." Assumption: "churn" = contract not renewed within 30 days of expiry, unless the data defines it otherwise — flag this and confirm later.

---

## 2. Stakeholder Mapping & Context

**Purpose:** Different stakeholders want different lenses on the same data (Tata's framing task made this explicit — CEO wants strategic view, CMO wants marketing/demographic view).

**Steps:**
1. List every stakeholder who will see or act on this analysis.
2. For each, note: their role, what decision *they* make, what metric or cut of the data they care about.
3. Identify where stakeholder interests conflict (e.g., ops wants cost reduction, marketing wants growth) — these tensions often shape which metrics matter most.

**Document:**
```
| Stakeholder | Role | Decision they'll make | What they need to see |
|---|---|---|---|
```

**Telco example:** CEO — needs churn's revenue impact and overall trend. Retention team — needs a ranked, actionable list of at-risk customers. Marketing — needs the demographic/segment profile of churners to target campaigns.

---

## 3. Hypothesis Development

**Purpose:** Go in with testable beliefs, not a blank slate — it keeps EDA focused and gives you something to confirm or reject rather than fish endlessly.

**Steps:**
1. From domain knowledge (or a quick literature/forum scan of how this problem is usually studied), write 3–5 hypotheses about what drives the outcome.
2. Phrase each so it's falsifiable: "Customers on month-to-month contracts churn at a higher rate than those on annual contracts."
3. Rank them by how much business impact confirming/rejecting each would have.

**Document:**
```
**H1:** ... — why I believe this — how I'll test it
**H2:** ...
**H3:** ...
```

**Telco example:** H1: Month-to-month contract customers churn more than long-term contract customers. H2: Customers with no tech support/add-on services churn more. H3: Tenure is inversely related to churn probability.

---

## 4. Data Acquisition / Extraction

**Purpose:** Know exactly where your data came from and its limitations before you trust anything downstream.

**Steps:**
1. Identify and log every data source (database, API, CSV export, third-party) and the access method.
2. Note the extraction window (date range) and any filters applied at the point of extraction.
3. Record row/column counts as a baseline you can sanity-check against later.
4. Note known limitations upfront (e.g., "only 12 months of history," "excludes cancelled-before-billing accounts").

**Document:**
```
**Source(s):**
**Extraction method (SQL/API/export):**
**Date range covered:**
**Baseline shape (rows x cols):**
**Known limitations:**
```

---

## 5. Data Cleaning

**Purpose:** Microsoft's cycle calls this "Prepare — Clean & Transform." This is where you make the data trustworthy — and where most silent errors get introduced if undocumented.

**Steps (document each one as you apply it — don't batch this at the end):**
1. **Structure check:** correct data types per column, consistent formatting (dates, currency, categorical labels).
2. **Missing values:** for each column with nulls — decide and log: drop, impute (and with what method/value), or flag as "unknown" category. State *why* for each.
3. **Duplicates:** check for and resolve duplicate records; log how many were found and the dedup logic used.
4. **Outliers/invalid values:** flag impossible values (negative tenure, age of 200); decide cap, remove, or investigate further.
5. **Consistency:** standardize categorical values (e.g., "Yes"/"yes"/"Y" → one label).
6. **Referential integrity:** if joining multiple tables later, confirm the join keys are clean now.

**Document (repeat this block per column or per issue found):**
```
**Column/issue:**
**Problem found:**
**Decision (drop/impute/cap/flag) and why:**
**Rows affected:**
```

---

## 6. Exploratory Data Analysis — the SCAN Framework

**Purpose:** Understand the business *through* the data. Use SCAN to keep this structured rather than aimless scrolling through charts.

**S — Stakeholder goals:** Revisit Stage 2. What KPIs and dimensions matter most to the people you mapped? Let this decide what you look at first.

**C — Columns and coverage:** What data do you actually have, and how usable is it? Which columns are complete, which are sparse, which are actually useful vs. noise?

**A — Aggregates and anomalies:** Compute the high-level metrics (overall churn rate, average tenure, revenue distribution). Look for outliers and unexpected patterns before slicing further.

**N — Notable segments:** Slice by category, time, or key dimensions (contract type, region, tenure band) to surface early signals — this is where your Stage-3 hypotheses get tested.

**Document (one pass per letter):**
```
**S — What matters to stakeholders, and what I'm prioritizing looking at:**
**C — Columns available / usability notes:**
**A — Key aggregate metrics and any anomalies found:**
**N — Segments explored and what stood out:**
**Hypotheses status:** H1 [supported/rejected/inconclusive] — evidence: ...
```

**Telco example under N:** Churn rate by contract type — confirms/rejects H1. Churn rate by tenure band — confirms/rejects H3.

---

## 7. Feature Engineering

**Purpose:** BCG X's framework — build features that make the "better" columns for your specific prediction target. Ask these four questions in order.

**Steps:**
1. **Remove:** Can we drop columns that are irrelevant, single-valued, or near-duplicates of another column? Log what you dropped and why.
2. **Expand:** Can we extract more signal from existing columns? (e.g., decompose a date into month/day-of-week/tenure-in-months; bucket a continuous variable into bands.)
3. **Combine:** Can we combine columns into a "better" column — one that's more predictive of the target? Define "better" concretely: does it improve model accuracy or interpretability? This is often iterative/experimental — log what you tried, even the things that didn't help.
4. **Combine datasets:** If merging multiple data sources, what's the join key, and does the merged data look sensible (row counts, no unexpected nulls introduced)?

**Document:**
```
**Removed columns:** — reason
**New features created:** — source columns — logic — hypothesis this supports
**Combinations tried that didn't help:** — why they were dropped
**Datasets merged:** — join key — resulting shape — sanity check performed
```

**Telco example:** New feature `services_count` = sum of add-on services subscribed (tests H2). New feature `tenure_band` = bucketed tenure (0–6mo, 6–24mo, 24mo+) to test non-linear tenure effects beyond raw H3.

---

## 8. Predictive Modeling & Evaluation

**Purpose:** Microsoft's "Model — Relationships & Logic" stage. Use the data to make predictions, and be honest about how reliable they are.

**Steps:**
1. **Define the target and framing:** classification or regression? What exactly is being predicted, and over what horizon?
2. **Split strategy:** train/validation/test split — and why (random, time-based, stratified).
3. **Baseline first:** always start with a naive baseline (majority class, simple rule) so later model lift is meaningful.
4. **Model selection:** which models tried, and why these (interpretability vs. performance trade-off, given your stakeholders).
5. **Evaluation metrics:** choose metrics that match the business cost from Stage 1 (e.g., recall matters more than precision if missing a churner is costlier than a false alarm).
6. **Interpretation:** feature importance / coefficients — do they align with your Stage-3 hypotheses? If not, investigate why before trusting the model.

**Document:**
```
**Target variable & definition:**
**Split strategy:**
**Baseline performance:**
**Models tried:** — key hyperparameters — why chosen
**Evaluation metric(s) chosen and why:**
**Final model performance:**
**Feature importance vs. hypotheses — do they agree?**
```

---

## 9. Insights & Recommendations

**Purpose:** Translate everything above into something a CEO/CMO (Stage 2 stakeholders) can act on. This is where your project-log entries get compiled and reframed — not new analysis, just clear communication.

**Steps:**
1. Answer the Stage-1 business question directly, in the first line.
2. For each stakeholder from Stage 2, translate the finding into what it means for *their* decision.
3. State recommendations as actions, not just findings ("target month-to-month customers with no tech support for retention offers" — not just "these customers churn more").
4. Be explicit about confidence and limitations — what would change your recommendation if wrong.

**Document:**
```
**Direct answer to the business question:**
**Recommendation(s) by stakeholder:**
**Confidence level and key limitations/caveats:**
**What I'd investigate next if given more time/data:**
```

---

## The Loop

Microsoft's cycle is a reminder that this isn't strictly linear — Manage (secure & govern) sits alongside every stage as a constant (data privacy, access control), and Analyze/Visualize often send you back to Feature Engineering or even Business Understanding as you learn more. When that happens, don't erase your earlier log entries — add a note: *"Revisited Stage X on [date] because [reason]."* That revision trail is itself valuable documentation of your thinking.

---

## Quick-Start Checklist (copy this at the top of every new project log)

- [ ] Stage 1 — Business problem written in one sentence
- [ ] Stage 2 — Stakeholder table complete
- [ ] Stage 3 — 3–5 falsifiable hypotheses written
- [ ] Stage 4 — Data source(s) and limitations logged
- [ ] Stage 5 — Every cleaning decision logged with reasoning
- [ ] Stage 6 — SCAN pass complete, hypotheses status updated
- [ ] Stage 7 — Feature engineering log complete (remove/expand/combine/merge)
- [ ] Stage 8 — Model, metric choice, and hypothesis-alignment logged
- [ ] Stage 9 — Recommendations written per stakeholder, confidence stated
