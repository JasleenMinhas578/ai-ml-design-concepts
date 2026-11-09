# Day 51: BONUS: Probability and Statistics

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Search a 2D Matrix (Binary search, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Scan every cell: O(m × n).

**Best approach:** Treat the matrix as one sorted list of length m·n; index i maps to (i // n, i % n). Binary search. O(log(m·n)).

```python
def searchMatrix(matrix, target):
    m, n = len(matrix), len(matrix[0])
    lo, hi = 0, m * n - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        v = matrix[mid // n][mid % n]
        if v == target: return True
        if v < target: lo = mid + 1
        else: hi = mid - 1
    return False
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A test for a rare disease is 99% accurate, and 1 in 1,000 people have it. If someone tests positive, the chance they're sick is only about 9%, because false positives from the 999 healthy people outnumber the true positives. That's Bayes' theorem.

### What to understand

**Distributions**  
Normal (bell curve), binomial (count of successes), Poisson (event counts per time), uniform.

**Mean, median, variance, std**  
Median resists outliers; std measures spread.

**Bayes' theorem**  
P(A|B) = P(B|A) × P(A) / P(B). Updates belief with evidence; base rates matter.

**Central limit theorem**  
Averages of many samples are roughly normal, whatever the original distribution.

**Hypothesis testing**  
Null hypothesis, p-value (chance of data this extreme if null is true), significance level 0.05.

**Type I and II errors**  
Type I = false positive; Type II = false negative. Power = 1 − Type II rate.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Explain a p-value simply.**  
If there were really no effect, how surprising would this data be? Small p = surprising.

**Q2. Why does the base rate matter?**  
With rare events, even accurate tests give many false positives.

**Q3. Mean vs median for salaries?**  
Median, since a few high earners skew the mean.

**Q4. What does the CLT let us do?**  
Use normal-based confidence intervals and tests for averages.

---

## Part 3: Out-loud check (15 min)

> Explain Bayes with the disease-test example.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Normal, binomial, Poisson
- Median resists outliers
- Bayes: base rates matter
- CLT → averages are normal
- p-value, Type I/II, power
