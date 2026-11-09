# Day 2: Linear Regression and Gradient Descent

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Contains Duplicate (Hash set, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Compare every pair: O(n²). Or sort and check neighbours: O(n log n).

**Best approach:** Walk the array; if a number is already in a set, return True, otherwise add it. O(n) time, O(n) space.

```python
def containsDuplicate(nums):
    seen = set()
    for n in nums:
        if n in seen:
            return True
        seen.add(n)
    return False
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A real-estate startup predicts house prices from size and location. With learning rate 1.0 the loss shoots to infinity; with 0.0001 it barely moves after an hour. At 0.01 it converges in minutes. Tuning the step size was the whole fix.

### What to understand

**Linear regression**  
Predicts a number as a weighted sum of features plus a bias: y = w·x + b.

**MSE loss**  
Mean of squared errors. Squaring punishes big errors more and makes the loss smooth to optimise.

**Gradient descent**  
Repeatedly move weights a small step against the gradient (the direction that increases loss most): w = w − lr × gradient.

**Learning rate**  
Step size. Too big: loss bounces or explodes. Too small: training is painfully slow.

**Batch vs mini-batch vs stochastic**  
Full batch uses all data per step (stable, slow). SGD uses one example (noisy, fast). Mini-batch (32–512) is the practical middle ground.

**Assumptions**  
Linear relationship, independent errors, constant variance, little multicollinearity. Violations hurt interpretation more than prediction.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Explain gradient descent to a non-technical person.**  
You're on a foggy hill and want the valley. Feel the slope under your feet and take a small step downhill. Repeat.

**Q2. What happens if the learning rate is too high?**  
Updates overshoot the minimum; loss oscillates or diverges.

**Q3. Why MSE instead of absolute error?**  
MSE is differentiable everywhere and penalises big errors more. MAE is more robust to outliers.

**Q4. What is multicollinearity and why does it matter?**  
Features strongly correlated with each other. Weights become unstable and hard to interpret; regularisation helps.

---

## Part 3: Out-loud check (15 min)

> Explain gradient descent and the effect of learning rate in 60 seconds.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- y = w·x + b
- MSE punishes big errors
- w = w − lr × gradient
- LR too high → diverges; too low → slow
- Mini-batch = practical default
