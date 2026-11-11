# Day 1: ML Workflow and Data Leakage

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Encode and Decode Strings (Hash/string, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Join strings with a separator like `,`. Breaks if a string contains a comma.

**Best approach:** Prefix each string with its length and a separator, e.g. `4#code`. To decode, read digits up to `#`, then read exactly that many characters. Works even if strings contain `#`.

```python
def encode(strs):
    return ''.join(f'{len(s)}#{s}' for s in strs)

def decode(s):
    res, i = [], 0
    while i < len(s):
        j = s.index('#', i)
        n = int(s[i:j])
        res.append(s[j+1:j+1+n])
        i = j + 1 + n
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A bank builds a loan-default model that scores 0.97 AUC offline but performs poorly live. The team finds a feature called `days_past_due_at_close`, which is only known after the loan ends. That's target leakage: the model learned the answer, not the risk. Removing it drops offline AUC to 0.81, which is the honest number.

### What to understand

**Problem framing**  
Turn a business goal into an ML task: what is the input, the label, and the success metric? Ask whether ML is even needed, or whether a rule would do.

**Train / validation / test split**  
Train fits the model, validation picks hyperparameters, test is touched once at the end to estimate real performance. Typical split is 70/15/15.

**Data leakage**  
Information from outside the training set sneaks into training, so scores look great offline and fail in production. Examples: scaling with stats from the full dataset, using a feature only known after the outcome, duplicate rows across splits.

**Target leakage vs train-test contamination**  
Target leakage = a feature encodes the answer (e.g. 'refund_issued' to predict fraud). Contamination = preprocessing or duplicates mix test data into training.

**Baselines**  
Always compare against something simple: predict the majority class, the mean, or a simple rule. If your model barely beats it, it isn't adding value.

**Time-based splits**  
For data with time, train on the past and test on the future. A random split leaks future information.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. What is data leakage and how do you prevent it?**  
Future or test information entering training. Prevent it by splitting first, fitting preprocessing only on train (use pipelines), and checking features exist at prediction time.

**Q2. Why do we need a validation set if we have a test set?**  
Tuning on the test set makes it optimistic. Validation is for choices; test is the final, untouched estimate.

**Q3. Your model has 99% accuracy. Should you be happy?**  
Not yet. Check class balance, the baseline, and leakage. On 99/1 data, predicting the majority gets 99%.

**Q4. How would you frame churn prediction as an ML problem?**  
Label = churned within next 30 days; features = usage before the cutoff date; metric = recall/precision at a chosen threshold; time-based split.

---

## Part 3: Out-loud check (15 min)

> Give one real example of data leakage and how to fix it.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Split first, preprocess second (fit on train only)
- Test set = touched once
- Leakage = info not available at prediction time
- Time data → time-based split
- Always beat a simple baseline

---

## Cheat sheet: what I learned today

**The ML workflow (churn example, music streaming app)**
1. **Frame the problem:** "Will this customer cancel in the next 30 days?" Binary classification. Ask why: the business wants to send discounts before people leave.
2. **Gather data and pick features:** listening hours, drop in usage, failed payments, support tickets, months subscribed. For each one, ask: would I know this on prediction day?
3. **Split by time:** train Jan–Sep, validate Oct, test Nov. Always predict the future from the past.
4. **Set a baseline:** "nobody churns" scores 95% accuracy if only 5% churn. My model must clearly beat it.
5. **Choose a metric:** recall (catch churners) plus precision (discounts cost money); PR-AUC overall. Not accuracy.
6. **Train and compare:** logistic regression, then XGBoost, compared on the **validation** set.
7. **Pick a threshold:** based on cost. Discount $5 vs lost customer $100, so some false alarms are fine.
8. **Test once, deploy, monitor:** run the test set once at the end, then watch for drift.

**Baseline (one sentence)**
"A baseline is the simplest possible guess, like predicting the majority class, and my model has to clearly beat it to prove it's actually learning something."

**Validation vs test (one sentence)**
"The validation set is for making decisions: tuning hyperparameters, comparing models and choosing a threshold. The test set is used only once at the end for an honest estimate. If I tuned on the test set, its score would look better than reality."
Validation = practice exams. Test = the real exam you sit once.

**Parameters vs hyperparameters**
- Parameters are **learned** during training: weights w and b in `price = w × size + b`, or the split rules in a tree.
- Hyperparameters are **set by me** before training: learning rate, number of training rounds, number of trees, max depth, regularisation strength.
- I pick hyperparameters by trying values and keeping the best on the validation set.
- Cake analogy: oven temperature and time = hyperparameters; how the cake rises = parameters.

**Data leakage**
- The model peeks at the answer during training. Like studying with the answer sheet mixed into your notes.
- **Target leakage:** a feature secretly contains the answer. Example: "takes insulin" to predict diabetes.
- **Train-test contamination:** test data sneaks into training, e.g. duplicate rows in both sets, or scaling with averages from the full dataset before splitting.

**Prediction time (the calendar picture)**
- Today is March 1; I predict who cancels in March. March 1 is the prediction time.
- Everything from February is fair to use. Anything from March is part of the answer.
- "Support calls in the last 30 days" is **safe** if counted only up to March 1. It leaks only if the window includes the March 10 "please cancel" call.
- A feature strongly linked to churn is not leakage by itself. The question is whether I'd have it at prediction time.

**How to fix leakage**
1. Split first, then clean, scale and build features.
2. Fit preprocessing on training data only (use scikit-learn pipelines).
3. Check every feature against prediction time.
4. Split by time when data has dates.
5. Remove duplicates; keep each customer in one split only.
6. Be suspicious of amazing scores.

Interview summary: **"Split first, fit only on train, and make sure every feature exists at prediction time."**

**Questions to ask before touching data (problem framing)**
1. How do we define churn: cancelling, or inactive for 30 days?
2. What's the time window: next week, month or quarter?
3. **What will we do with the predictions?** (Most important: it decides how many false alarms we can afford.)
4. How do we measure success: retained revenue, recall, PR-AUC?
5. What data do we have, and how many past churners?
6. Is there a current rule or baseline already?

**Practice questions I answered**
- *98% accuracy but catches no churners?* Class imbalance; accuracy is the wrong metric. Fix: recall/PR-AUC, compare to baseline, class weights or lower threshold. Also check for leakage and drift.
- *Is "support calls in the last 30 days" safe?* Yes, if counted only up to the prediction date.
- *What would you ask before starting?* The six framing questions above.
