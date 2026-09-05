# THE DATA PROJECT OPERATING SYSTEM
## A beginner-friendly, professional workflow for analytics and data science projects

### Purpose

This framework is designed to answer one question:

> **"When I receive a new data project, how do I know what to do next?"**

It is not a checklist for producing code.

It is a **decision-making system**.

The objective is to develop the habit of thinking like a professional analyst/data scientist:

**Business → Decision → Question → Data → Evidence → Analysis → Decision → Action**

Do not start with Python.

Do not start with SQL.

Do not start with visualization.

Do not start with machine learning.

Start with the problem.

---

# THE 8 GATES

Every project passes through these gates:

```text
GATE 1
WHY?
What problem are we trying to solve?

        ↓

GATE 2
WHAT?
What exactly are we trying to learn?

        ↓

GATE 3
CAN WE ANSWER IT?
Is this question measurable and feasible?

        ↓

GATE 4
DATA
Do we have the right data?

        ↓

GATE 5
EXPLORE
What does the data actually tell us?

        ↓

GATE 6
ANALYZE
What evidence answers the question?

        ↓

GATE 7
DECIDE
What should someone do because of this?

        ↓

GATE 8
COMMUNICATE
Can another person understand and trust the conclusion?
```

These gates are **not perfectly linear**.

You will often go:

```text
Explore
   ↓
discover problem with data
   ↓
return to Question
   ↓
change analysis
```

That is normal.

Professional analysis is iterative.

---

# GATE 1 — WHY?

## Business / Problem Understanding

### Objective

Understand why the project exists before touching the data.

Ask:

1. What problem exists?
2. Who has the problem?
3. Why does it matter?
4. What decision needs to be made?
5. What happens if nothing changes?
6. What would someone do differently if we knew the answer?

### The most important question

> **"What decision will this analysis help someone make?"**

If you cannot answer this, you are not ready for analysis.

---

## Convert the vague request

Stakeholder says:

> "Analyze customer churn."

Do NOT immediately open Python.

Translate it.

Possible interpretation:

> "The business wants to understand which customer segments have unusually high churn so the retention team can decide where to focus intervention."

Now you have something actionable.

---

## Write this

```text
BUSINESS PROBLEM:

The problem is...

WHY IT MATTERS:

This matters because...

DECISION:

The analysis will help ______ decide ______.

IDEAL OUTCOME:

We would like to know ______ so that ______.

STAKEHOLDER:

The person/team who will use this is ______.

CONSEQUENCE OF BEING WRONG:

If our conclusion is wrong, ______.
```

---

## GATE 1 DECISION

Ask:

> **Can I clearly explain the problem and the decision this project supports?**

YES → Continue.

NO → Stop and clarify the problem.

---

# GATE 2 — WHAT?

## Question Definition

Now turn the business problem into analytical questions.

Do NOT immediately create ten questions.

Start with:

### Primary question

> What is the ONE question this project must answer?

Then create supporting questions.

Example:

### Primary question

> What factors are associated with customer churn?

### Supporting questions

```text
1. What is the overall churn rate?
2. How does churn vary by contract type?
3. How does churn vary with tenure?
4. Which customer segments have the highest churn?
5. Are there meaningful changes over time?
6. Which factors remain important after controlling for other variables?
```

---

# QUESTION TREE

Use this whenever you don't know what to investigate.

```text
                     BUSINESS PROBLEM
                            │
                            ▼
                     PRIMARY QUESTION
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
          DESCRIPTIVE   DIAGNOSTIC   PREDICTIVE
          What happened? Why?        What will happen?
              │             │             │
              ▼             ▼             ▼
          Metrics       Comparisons    Models
          Trends        Segments       Forecasts
          Distributions Relationships  Classification
```

You do not automatically need all three.

Choose the type that matches the decision.

---

# ANALYTICAL QUESTION TYPES

## Descriptive

> What happened?

Examples:

- How many customers churned?
- What was monthly revenue?
- Which province had the highest positivity rate?

## Diagnostic

> Why / what is associated with it?

Examples:

- Which factors are associated with churn?
- Why did sales decline?
- Which customer segments behave differently?

## Predictive

> What is likely to happen?

Examples:

- Which customers are likely to churn?
- What will demand be next month?

## Prescriptive

> What should we do?

Examples:

- Which customers should receive an intervention?
- Which product should receive additional investment?

---

# GATE 2 DECISION

Ask:

> **Can I state the exact analytical question in one sentence?**

If not:

STOP.

Rewrite the question.

---

# GATE 3 — CAN WE ANSWER IT?

## Feasibility

This is the gate missing from many beginner workflows.

Before spending hours analyzing data, ask:

### 1. Is the question measurable?

Can the desired outcome actually be represented by data?

### 2. Do we have the necessary data?

### 3. Is the data at the correct level?

For example:

```text
Question:
Which customers churn?

Data:
Monthly aggregate revenue by province
```

Wrong grain.

You cannot answer a customer-level question with province-level data.

### 4. Is there enough historical coverage?

### 5. Are important variables missing?

### 6. Is there leakage?

### 7. Is the requested analysis technically possible?

### 8. Is the answer useful enough to justify the effort?

Google explicitly recommends considering feasibility, including data availability, problem difficulty, prediction quality, technical requirements, and cost when planning ML projects.

---

# FEASIBILITY CHECK

```text
QUESTION:
________________________________

UNIT OF ANALYSIS:
________________________________

TARGET / OUTCOME:
________________________________

TIME PERIOD:
________________________________

REQUIRED VARIABLES:
________________________________

AVAILABLE VARIABLES:
________________________________

MISSING VARIABLES:
________________________________

DATA GRANULARITY:
________________________________

KNOWN LIMITATIONS:
________________________________

CAN THIS QUESTION BE ANSWERED?

[ ] YES
[ ] PARTIALLY
[ ] NO

IF NO, WHY?
________________________________
```

---

# GATE 3 DECISION

```text
ANSWERABLE?
       │
 ┌─────┴─────┐
YES          NO
 │            │
 ▼            ▼
Continue     Redefine
```

Never force a dataset to answer a question it cannot answer.

---

# GATE 4 — DATA

## Understand Before Cleaning

Now inspect the data.

The goal is NOT:

> "Make the dataset clean."

The goal is:

> **"Determine whether this data is trustworthy enough to answer my question."**

---

# STEP 1 — DATA INVENTORY

Record:

```text
SOURCE:

TABLE / FILE:

ROWS:

COLUMNS:

TIME PERIOD:

UNIT OF OBSERVATION:

PRIMARY KEY:

IMPORTANT VARIABLES:
```

---

# STEP 2 — UNDERSTAND THE GRAIN

This is one of the most important professional habits.

Ask:

> **What does one row represent?**

Examples:

```text
One row = one customer

One row = one transaction

One row = one order

One row = one patient visit

One row = one day

One row = one province per day
```

If you don't understand the grain, don't analyze yet.

---

# STEP 3 — DATA QUALITY

Check:

```text
Missing values
Duplicates
Invalid values
Incorrect data types
Impossible values
Outliers
Inconsistent categories
Date problems
Join problems
Unexpected cardinality
```

But don't blindly "fix" things.

For every problem ask:

> What does this represent?

> Why did it happen?

> What effect could it have on my conclusion?

---

# STEP 4 — VALIDATE THE DATA

Before trusting the dataset:

```text
Does the row count make sense?

Do totals match known totals?

Do dates make sense?

Are categories complete?

Are there impossible values?

Do joins increase/decrease rows unexpectedly?

Do calculated metrics agree with known values?
```

Google's guidance similarly emphasizes validating new metrics against known data/features before using them to make new discoveries.

---

# GATE 4 DECISION

Ask:

> **Do I understand where the data came from, what each row represents, and whether the data is trustworthy enough for my question?**

YES → Continue.

NO → Investigate.

---

# GATE 5 — EXPLORE

## EDA

This is where your existing SCAN framework is useful.

But use EDA for a purpose.

Do not make 47 charts because you can.

Your EDA should answer:

> **"What do I need to understand about this data before I can answer my question?"**

---

# THE EDA ORDER

## 1. BIG PICTURE

Start with:

```text
How large is the dataset?

What period does it cover?

What is the target/outcome distribution?

What are the major categories?

What does the overall trend look like?
```

---

## 2. DISTRIBUTIONS

Understand:

```text
Numerical variables
Categorical variables
Target variable
Time variables
```

Ask:

> What does "normal" look like in this dataset?

---

## 3. SEGMENTS

Break the outcome down by important dimensions.

For example:

```text
Overall churn
      ↓
By contract
      ↓
By tenure
      ↓
By geography
      ↓
By service
      ↓
By combinations of important variables
```

---

## 4. TIME

Always ask:

> Does the behaviour change over time?

Look for:

```text
Trend
Seasonality
Sudden changes
Structural breaks
Missing periods
Data collection changes
```

---

## 5. ANOMALIES

When you find something strange:

DO NOT immediately delete it.

Ask:

> Is this an error or a real phenomenon?

That distinction is critical.

---

# EDA RULE

Every chart should answer a question.

Before creating a visualization, write:

```text
QUESTION:
What am I trying to learn?

VISUAL:
What chart will help answer it?

OBSERVATION:
What do I see?

INTERPRETATION:
What might explain it?

NEXT STEP:
What should I investigate?
```

This prevents "chart wandering."

---

# GATE 5 DECISION

Ask:

> **Do I understand the structure, behaviour, anomalies and major patterns in the data?**

If yes → move to analysis.

If no → continue exploring.

---

# GATE 6 — ANALYZE

Now investigate the actual question.

This is where you choose your analytical method.

## DO NOT choose the method first.

Choose it based on the question.

---

# METHOD SELECTION TREE

```text
WHAT DO I NEED TO KNOW?
          │
          ├── What happened?
          │       ↓
          │   Descriptive analysis
          │
          ├── How are groups different?
          │       ↓
          │   Comparison / segmentation
          │
          ├── Are variables related?
          │       ↓
          │   Statistical analysis
          │
          ├── Why might something be happening?
          │       ↓
          │   Diagnostic analysis
          │
          ├── What will happen?
          │       ↓
          │   Predictive modeling
          │
          └── What should we do?
                  ↓
              Decision analysis
```

---

# ANALYSIS LOOP

For every important finding:

```text
OBSERVATION
     ↓
QUESTION
     ↓
ANALYSIS
     ↓
EVIDENCE
     ↓
INTERPRETATION
     ↓
VALIDATION
     ↓
CONCLUSION
```

Never jump:

```text
Observation → Conclusion
```

Example:

> Churn is higher among month-to-month customers.

That is an observation.

Do not immediately conclude:

> Therefore month-to-month contracts cause churn.

Instead ask:

```text
Could tenure explain this?

Could pricing explain this?

Could customer type explain this?

Could acquisition channel explain this?

Could there be selection bias?

Could the relationship disappear after controlling for other variables?
```

This is where professional analytical thinking develops.

---

# HYPOTHESES

Your original framework puts hypotheses very early.

I would change that.

Use **two types of hypotheses**.

### Before EDA

Use broad expectations.

Example:

> I expect churn to differ across contract types.

### During EDA

Allow the data to generate new hypotheses.

Example:

> I discovered that churn spikes during the first six months. I will investigate whether onboarding/service issues explain this.

This is more realistic than pretending you know all the important hypotheses before seeing the data.

Google's own guidance describes complex analysis as iterative: anomalies and trends can lead to theories, which should then be tested against evidence rather than simply accepted.

---

# ANALYTICAL VALIDATION

For important findings ask:

```text
Is this statistically meaningful?

Is this practically meaningful?

Could this be caused by another variable?

Could this be a data-quality issue?

Does the result hold across reasonable slices?

Does the result hold over time?

Would another reasonable method produce a similar conclusion?
```

---

# IF MACHINE LEARNING IS REQUIRED

Only enter the ML branch if the problem actually requires prediction/automation.

```text
Problem
   ↓
Can a simple rule solve it?
   ↓
YES → Don't automatically use ML
NO
   ↓
Define target
   ↓
Define prediction horizon
   ↓
Define success metric
   ↓
Split data
   ↓
Baseline
   ↓
Simple model
   ↓
Evaluate
   ↓
Feature engineering
   ↓
More models
   ↓
Tune
   ↓
Final evaluation
```

Google explicitly treats problem framing as determining whether ML is appropriate in the first place, rather than assuming every problem should become an ML problem.

---

# ML GOLDEN RULE

Never ask:

> "Which model should I use?"

Ask:

> "What decision am I trying to improve, and what prediction would help make that decision?"

---

# GATE 6 DECISION

Ask:

> **Do I have sufficient evidence to answer the original question?**

YES → Continue.

NO → Return to:

```text
Question
   ↓
Data
   ↓
EDA
   ↓
Analysis
```

---

# GATE 7 — DECIDE

This is where analysis becomes valuable.

Separate:

### FACT

What the data directly shows.

### INTERPRETATION

What you believe explains the finding.

### RECOMMENDATION

What someone should do.

Example:

```text
FACT:
Customers with X had a 28% churn rate.

INTERPRETATION:
This may indicate that X is associated with higher churn.

RECOMMENDATION:
Test a retention intervention for this segment.
```

Do not confuse these three.

---

# THE DECISION TEST

For every major finding ask:

> **"So what?"**

Then ask again:

> **"What would someone actually do with this information?"**

If you cannot answer those questions, the analysis may not yet be useful.

---

# RECOMMENDATION FRAMEWORK

Every recommendation should contain:

```text
ACTION:
What should happen?

TARGET:
Who/what should be affected?

REASON:
What evidence supports this?

EXPECTED BENEFIT:
What should improve?

RISK:
What could go wrong?

MEASUREMENT:
How will we know it worked?
```

---

# GATE 7 DECISION

Ask:

> **Can my findings change a real decision or improve understanding of the problem?**

If yes → communicate.

If no → determine whether more analysis is required.

---

# GATE 8 — COMMUNICATE

Your final output should NOT be:

> "Here are my charts."

It should be a story.

---

# THE PROFESSIONAL STORY

```text
1. BUSINESS PROBLEM

What were we trying to solve?

        ↓

2. APPROACH

What did we analyze?

        ↓

3. KEY FINDING

What did we discover?

        ↓

4. EVIDENCE

Why should we believe it?

        ↓

5. BUSINESS MEANING

Why does it matter?

        ↓

6. RECOMMENDATION

What should happen?

        ↓

7. LIMITATIONS

What don't we know?

        ↓

8. NEXT STEP

What should happen next?
```

---

# THE ONE-PAGE PROJECT SUMMARY

Every finished project should eventually be reducible to this:

```text
# PROJECT

## 1. Problem
What problem were we solving?

## 2. Decision
What decision did the analysis support?

## 3. Data
What data did we use?

## 4. Method
How did we analyze it?

## 5. Key Findings
What did we discover?

## 6. Evidence
What supports those findings?

## 7. Recommendation
What should be done?

## 8. Limitations
What could make the conclusion wrong?

## 9. Next Step
What should happen next?
```

---

# THE PROFESSIONAL THINKING LOOP

This is the part I want you to memorize.

When you get stuck, ask these questions:

```text
1. WHAT AM I TRYING TO FIND OUT?

        ↓

2. WHY DOES IT MATTER?

        ↓

3. WHAT DECISION WILL THIS INFORM?

        ↓

4. WHAT WOULD I EXPECT TO SEE IF MY THEORY IS TRUE?

        ↓

5. WHAT DATA WOULD ALLOW ME TO TEST THAT?

        ↓

6. IS THE DATA ACTUALLY CAPABLE OF ANSWERING IT?

        ↓

7. WHAT DOES THE DATA SHOW?

        ↓

8. COULD THERE BE ANOTHER EXPLANATION?

        ↓

9. WHAT EVIDENCE WOULD CHANGE MY MIND?

        ↓

10. SO WHAT?

        ↓

11. WHAT SHOULD SOMEONE DO?

        ↓

12. HOW CONFIDENT AM I?
```

This is your **mental operating system**.

---

# THE "I DON'T KNOW WHAT TO DO NEXT" PROTOCOL

When you get stuck during a project, DO NOT randomly try another Python function.

Stop and identify where you are.

### If you don't know what to investigate:

Return to:

> **What question am I trying to answer?**

### If you don't know which columns to examine:

Return to:

> **What variables could plausibly influence the outcome?**

### If you don't know which chart to make:

Return to:

> **What question would this chart answer?**

### If you find something interesting:

Ask:

> **Is this real, or could it be an artifact?**

### If you find a relationship:

Ask:

> **What alternative explanations exist?**

### If you have a model:

Ask:

> **Does this model improve the decision?**

### If you have a result:

Ask:

> **So what?**

### If you have a recommendation:

Ask:

> **What evidence supports it?**

---

# PROJECT DECISION TREE

Use this at the beginning of EVERY project.

```text
START
  │
  ▼
What problem are we solving?
  │
  ├── I DON'T KNOW
  │       ↓
  │   Clarify problem
  │
  ▼
What decision will this support?
  │
  ├── I DON'T KNOW
  │       ↓
  │   Clarify stakeholder need
  │
  ▼
What question answers that decision?
  │
  ├── I DON'T KNOW
  │       ↓
  │   Define analytical question
  │
  ▼
Can the question be answered with data?
  │
  ├── NO
  │       ↓
  │   Redefine question
  │
  ▼
Do we have the required data?
  │
  ├── NO
  │       ↓
  │   Find data / change scope
  │
  ▼
Do we understand the data?
  │
  ├── NO
  │       ↓
  │   Data investigation
  │
  ▼
Is the data trustworthy?
  │
  ├── NO
  │       ↓
  │   Investigate quality
  │
  ▼
Explore
  │
  ▼
What patterns/questions emerge?
  │
  ▼
Analyze
  │
  ▼
Validate
  │
  ▼
Answer the question
  │
  ▼
So what?
  │
  ▼
Recommendation
  │
  ▼
Communicate
  │
  ▼
END
```

---

# PROJECT LOG

Do NOT document every line of code.

Document decisions.

For each major decision:

```text
DATE:

DECISION:

WHAT I DID:

WHY I DID IT:

EVIDENCE:

RESULT:

WHAT THIS CHANGED:

ALTERNATIVES CONSIDERED:

WHAT COULD MAKE THIS WRONG:
```

This is much more valuable than a notebook full of comments.

---

# THE 5 QUESTIONS YOU SHOULD ALWAYS WRITE DOWN

At the beginning of a project:

```text
1. WHAT AM I TRYING TO ANSWER?

2. WHY DOES IT MATTER?

3. WHAT DATA WOULD I NEED?

4. WHAT WOULD COUNT AS GOOD EVIDENCE?

5. WHAT DECISION WILL THIS ENABLE?
```

If you can answer those five questions, you have the foundation of the project.

---

# IMPORTANT PRINCIPLES

## Principle 1 — Business before tools

Never:

```text
"I have a dataset. What model can I build?"
```

Prefer:

```text
"There is a problem. What can the data tell us?"
```

---

## Principle 2 — Questions before charts

Never create a chart just because the data contains a column.

Every visualization should have a question behind it.

---

## Principle 3 — Evidence before conclusions

Never jump from:

```text
I observed X
```

to:

```text
Therefore X causes Y.
```

---

## Principle 4 — Simple before complex

Start with:

```text
Simple metric
     ↓
Simple comparison
     ↓
Simple statistical analysis
     ↓
Simple baseline
     ↓
More complex method
```

Complexity must earn its place.

---

## Principle 5 — Validate before trusting

Every important result should survive reasonable challenges.

---

## Principle 6 — Analysis is iterative

Do not expect:

```text
Question → Data → EDA → Answer
```

to happen once.

Real projects often look like:

```text
Question
   ↓
Data
   ↓
EDA
   ↓
Interesting finding
   ↓
New question
   ↓
More data
   ↓
New analysis
   ↓
Validation
   ↓
Conclusion
```

---

## Principle 7 — The model is not the product

The product is the improved decision.

A model that achieves impressive accuracy but doesn't improve a real decision is not necessarily a successful data science project.

---

# BEGINNER RULE

When learning, your objective is NOT:

> "Finish projects as quickly as possible."

Your objective is:

> **"Learn to make good analytical decisions."**

Every project should therefore teach you:

```text
How to scope
How to question
How to inspect
How to validate
How to reason
How to choose methods
How to communicate
```

The Python, SQL, statistics, visualization and ML techniques are tools inside that process.

---

# THE FINAL FRAMEWORK

Memorize this:

## WHY → WHAT → CAN → DATA → EXPLORE → ANALYZE → DECIDE → COMMUNICATE

### WHY
What problem are we solving?

### WHAT
What exactly do we need to know?

### CAN
Can the question actually be answered?

### DATA
Do we have trustworthy data?

### EXPLORE
What does the data reveal?

### ANALYZE
What evidence answers the question?

### DECIDE
What should happen because of the evidence?

### COMMUNICATE
Can another person understand, trust and act on the conclusion?

---

# THE GOLDEN QUESTION

Whenever you don't know what to do next:

> **"What do I need to know right now in order to make the next good decision?"**

Then do only the analysis necessary to answer that question.

That is the habit this framework is designed to build.