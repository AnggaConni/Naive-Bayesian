# Bayesian Analysis Framework Guide

> **Methodology Reference**  
> A comprehensive guide explaining how this application updates beliefs using evidence — including the meaning of **Confidence**, how **Likelihood Ratios** work, and when to use **Naive Bayes** versus a **Bayesian Network**.

---

# Core Principle of This Application

> ⚠ **Architecture Notice**  
> This application is built on a **Naive Bayes architecture**.  
> It assumes that every piece of evidence entered is **conditionally independent** from other evidence given the hypothesis.

Bayesian reasoning updates beliefs when new evidence appears.

You start with:

- **Prior** → what you believe before seeing evidence  
- **Posterior** → what you believe after evaluating evidence

This application updates beliefs **iteratively**, meaning each evidence item updates the probability step-by-step.

---

# 1. How the Calculation Works

The engine converts the **prior probability into odds**, multiplies each evidence contribution, then converts back to probability.

### Master Formula

```
Posterior Odds = Prior Odds × ∏ ( LRᵢ ^ confidenceᵢ )
```

### Step-by-step logic

1️⃣ Convert prior probability to odds

```
Odds = P / (1 − P)
```

2️⃣ Compute the effective Likelihood Ratio

```
LR_eff = LR ^ confidence
```

3️⃣ Multiply the running odds

```
Odds_new = Odds_old × LR_eff
```

4️⃣ Convert back to probability

```
Posterior Probability = Odds / (1 + Odds)
```

---

## Worked Example

**Prior**

```
P = 0.40
Odds = 0.40 / 0.60 = 0.667
```

**Evidence 1**

```
LR = 3.0
Confidence = 0.8

LR_eff = 3 ^ 0.8 = 2.41
New Odds = 0.667 × 2.41 = 1.607
```

**Evidence 2**

```
LR = 0.5
Confidence = 1.0

LR_eff = 0.5
New Odds = 1.607 × 0.5 = 0.804
```

**Final Posterior**

```
P = 0.804 / (1 + 0.804)
P ≈ 0.446
```

---

# 2. Hypothesis

The **Hypothesis** is the claim you want to evaluate.

A good hypothesis must be:

- clear
- falsifiable
- testable using observable evidence

### Example Hypothesis

> *Village development policies focusing heavily on physical infrastructure may unintentionally increase income inequality among residents.*

All evidence entered in the system is evaluated **relative to this hypothesis**.

---

# 3. Prior Probability

The **Prior** represents your belief **before reviewing the current evidence**.

Suggested interpretation:

| Prior | Meaning |
|------|--------|
| **0.50** | Neutral starting point |
| **0.30** | Hypothesis initially unlikely |
| **0.70** | Hypothesis initially plausible |
| **0.10–0.20** | Strong prior skepticism |
| **0.80–0.90** | Strong prior belief |

⚠ **Important**

A biased prior will distort the posterior result.  
When unsure, **use 0.50** and let the evidence update the probability.

---

# 4. Decision Threshold

The **Decision Threshold** defines when the posterior probability becomes strong enough to support a conclusion or action.

Typical thresholds:

| Threshold | Interpretation |
|----------|---------------|
| **0.60** | Exploratory analysis |
| **0.70 – 0.75** | Moderate policy confidence |
| **0.80 – 0.85** | Strong evidence for decision making |
| **0.90+** | Extremely high certainty required |

Choosing a threshold depends on the **risk of being wrong**.

- **False Positive** → Acting when the hypothesis is false  
- **False Negative** → Ignoring a true hypothesis

Higher-stakes decisions require **higher thresholds**.

---

# 5. Likelihood Ratios (LR)

A **Likelihood Ratio** expresses how strongly evidence supports or contradicts the hypothesis.

| LR Value | Interpretation |
|--------|---------------|
| **>10** | Very strong support |
| **3 – 10** | Moderate support |
| **1 – 3** | Weak support |
| **1** | Neutral evidence |
| **0.3 – 1** | Weak contradiction |
| **0.1 – 0.3** | Moderate contradiction |
| **<0.1** | Strong contradiction |

Example:

```
LR = 5
```

means the evidence is **5 times more likely if the hypothesis is true** than if it is false.

---

# 6. Confidence

Confidence reflects **how reliable you believe the evidence is**.

Confidence acts as a **dampening exponent** applied to the LR:

```
Effective LR = LR ^ Confidence
```

Confidence scale:

| Confidence | Meaning |
|-----------|--------|
| **1.0** | Fully trusted evidence |
| **0.8** | Strong but imperfect evidence |
| **0.6** | Moderate reliability |
| **0.4** | Weak reliability |
| **0.2** | Very uncertain evidence |

Example:

```
LR = 5
Confidence = 0.5

LR_eff = 5^0.5 ≈ 2.24
```

This reduces the impact of uncertain evidence.

---

# 7. Evidence Independence (Naive Bayes Assumption)

Naive Bayes assumes:

> Evidence items are **conditionally independent given the hypothesis**.

This means:

```
P(E1, E2 | H) = P(E1 | H) × P(E2 | H)
```

In real-world analysis this assumption is sometimes imperfect, but the model works well when:

- evidence sources are reasonably independent
- evidence types differ (data, testimony, statistics, observation)

---

# 8. When to Use a Full Bayesian Network

Naive Bayes is simple and fast, but cannot model **dependencies between evidence**.

Use a **Bayesian Network** if:

- evidence items influence each other
- causal relationships exist between variables
- multiple hypotheses interact

However, Bayesian Networks require:

- complex structure design
- conditional probability tables
- significantly more data

For most analytical workflows, **Naive Bayes offers an excellent balance of simplicity and rigor.**

---

# Summary

**This tool implements a structured evidence reasoning process:**

1. Define a **Hypothesis**
2. Set a **Prior**
3. Enter **Evidence**
4. Assign **Likelihood Ratios**
5. Adjust using **Confidence**
6. Compute the **Posterior Probability**
7. Compare against the **Decision Threshold**

The result is a **transparent and auditable chain of reasoning**.

---

© Bayesian Evidence Analysis Guide
