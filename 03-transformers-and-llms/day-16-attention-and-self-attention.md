# Day 16: Attention and Self-Attention

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Valid Parentheses (Stack, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Repeatedly remove '()', '[]', '{}' pairs until nothing changes: O(n²).

**Best approach:** Push opening brackets; on a closing bracket, the top of the stack must be its match. Stack must be empty at the end.

```python
def isValid(s):
    pairs = {')': '(', ']': '[', '}': '{'}
    stack = []
    for ch in s:
        if ch in pairs:
            if not stack or stack.pop() != pairs[ch]:
                return False
        else:
            stack.append(ch)
    return not stack
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

In 'The trophy didn't fit in the suitcase because it was too big', the model must know 'it' means the trophy. Self-attention lets 'it' put high weight on 'trophy', so the representation of 'it' carries that meaning.

### What to understand

**Query, Key, Value**  
Each token makes a query (what I'm looking for), a key (what I contain) and a value (what I pass on).

**Scaled dot-product attention**  
softmax(QKᵀ / √d) · V. Scores how relevant every token is to every other, then mixes their values.

**Why divide by √d**  
Keeps dot products from growing too large, which would make softmax too peaky and gradients tiny.

**Multi-head attention**  
Several attention heads in parallel, each learning different relationships (syntax, coreference, etc.).

**Positional encoding**  
Attention ignores order, so position information is added (sinusoidal, learned, or RoPE).

**Causal mask and complexity**  
Decoders mask future tokens so they can't peek. Attention costs O(n²) in sequence length.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Explain self-attention simply.**  
Each word looks at every other word, decides how relevant each is, and builds a new representation from the relevant ones.

**Q2. Why multiple heads?**  
Each head can focus on a different type of relationship.

**Q3. Why do transformers need positional encoding?**  
Attention treats input as a set; without positions, word order is lost.

**Q4. What's the cost of attention with long inputs?**  
Quadratic in sequence length, which limits context size.

---

## Part 3: Out-loud check (15 min)

> Draw and explain self-attention in 2 minutes.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- softmax(QKᵀ/√d)·V
- Q = what I want, K = what I have, V = what I give
- Multi-head = many relationship types
- Positional encoding adds order
- Cost O(n²) in length; causal mask in decoders
