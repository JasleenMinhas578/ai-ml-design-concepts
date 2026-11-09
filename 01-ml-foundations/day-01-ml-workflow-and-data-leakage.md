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
