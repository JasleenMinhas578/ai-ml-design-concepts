# Day 10: Neural Network Fundamentals

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Valid Palindrome (Two pointers, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Clean the string, then compare to its reverse. Uses extra memory.

**Best approach:** Pointers at both ends; skip non-alphanumeric characters; compare lowercase characters moving inward.

```python
def isPalindrome(s):
    l, r = 0, len(s) - 1
    while l < r:
        while l < r and not s[l].isalnum():
            l += 1
        while l < r and not s[r].isalnum():
            r -= 1
        if s[l].lower() != s[r].lower():
            return False
        l += 1; r -= 1
    return True
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A team trains a 20-layer network with sigmoid activations and the early layers stop learning: gradients vanish. Switching to ReLU, He initialisation and batch norm gets it training normally.

### What to understand

**Neuron and layer**  
Each neuron computes a weighted sum plus bias, then an activation. Layers stack these.

**Activations**  
ReLU = max(0, x), the default for hidden layers. Sigmoid for binary output; softmax for multi-class output.

**Forward pass**  
Inputs flow through layers to produce a prediction and a loss.

**Backpropagation**  
The chain rule applied backwards through the network to get each weight's gradient.

**Vanishing / exploding gradients**  
Gradients shrink or blow up through many layers. Fixes: ReLU, good init, batch/layer norm, residual connections, gradient clipping.

**Why non-linearity**  
Without activations, stacked layers collapse into one linear model.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Why did ReLU help deep networks?**  
Its gradient is 1 for positive inputs, so it doesn't vanish like sigmoid's, and it's cheap.

**Q2. What is backpropagation?**  
Using the chain rule to compute how much each weight contributed to the loss, from output back to input.

**Q3. What is the dying ReLU problem?**  
Neurons stuck outputting 0 never update; Leaky ReLU or GELU help.

**Q4. Why do we need activation functions?**  
They add non-linearity so the network can learn complex patterns.

---

## Part 3: Out-loud check (15 min)

> Explain backprop and why ReLU helps, without notes.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Neuron = weighted sum + activation
- No activation → just linear
- Backprop = chain rule backwards
- ReLU default; softmax for classes
- Vanishing gradients → ReLU, norm, residuals
