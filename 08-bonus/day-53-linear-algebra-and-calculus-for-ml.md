# Day 53: BONUS: Linear Algebra and Calculus for ML

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Permutations (Backtracking, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Use itertools.permutations: fine in practice, but learn the backtracking version.

**Best approach:** Backtrack: build a path, try each unused number, recurse, then undo.

```python
def permute(nums):
    res = []
    def bt(path, used):
        if len(path) == len(nums):
            res.append(path[:]); return
        for i in range(len(nums)):
            if not used[i]:
                used[i] = True; path.append(nums[i])
                bt(path, used)
                path.pop(); used[i] = False
    bt([], [False] * len(nums))
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

When an interviewer asks 'What is attention, mathematically?', you can say: a matrix multiplication of queries and keys gives similarity scores, softmax turns them into weights, and another matrix multiplication mixes the values. That's all linear algebra.

### What to understand

**Vectors and dot product**  
The dot product measures alignment; it's the core of similarity search and attention.

**Matrix multiplication**  
A layer in a neural network is a matrix multiply plus bias. Know shape rules: (m×n)·(n×p) = (m×p).

**Eigenvectors and SVD**  
Directions a matrix only stretches; PCA uses them. SVD also underlies low-rank ideas like LoRA.

**Derivatives and gradients**  
Rate of change; the gradient points uphill, so we step the opposite way.

**Chain rule**  
Derivative of nested functions; it's what backprop computes.

**Norms**  
L1 and L2 lengths; used in regularisation and distances.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. What does a dot product tell you?**  
How aligned two vectors are; high = similar direction.

**Q2. How does LoRA relate to linear algebra?**  
It approximates a weight update with two small low-rank matrices.

**Q3. Why do we need the chain rule in deep learning?**  
Networks are nested functions; the chain rule gives each weight's gradient.

**Q4. What does PCA compute?**  
Eigenvectors of the covariance matrix: the directions of most variance.

---

## Part 3: Out-loud check (15 min)

> Explain attention and LoRA using dot products and low rank.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Dot product = similarity
- Layer = matrix multiply + bias
- Shapes: (m×n)(n×p)
- Eigenvectors → PCA; low rank → LoRA
- Chain rule = backprop
