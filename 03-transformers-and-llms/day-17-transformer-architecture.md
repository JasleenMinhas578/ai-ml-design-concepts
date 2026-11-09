# Day 17: Transformer Architecture

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Min Stack (Stack, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Store values; scan the whole stack for the minimum: O(n) getMin.

**Best approach:** Keep a second stack (or pairs) storing the current minimum at each push. All operations O(1).

```python
class MinStack:
    def __init__(self):
        self.stack = []  # (value, current_min)
    def push(self, val):
        m = min(val, self.stack[-1][1]) if self.stack else val
        self.stack.append((val, m))
    def pop(self):
        self.stack.pop()
    def top(self):
        return self.stack[-1][0]
    def getMin(self):
        return self.stack[-1][1]
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A company needs to classify support emails and also draft replies. They use a fine-tuned BERT-style encoder to route emails (fast, cheap, accurate) and a decoder LLM to write the replies.

### What to understand

**Transformer block**  
Multi-head attention → add and layer norm → feed-forward network → add and layer norm.

**Residual connections**  
Add the input back to the output of each sub-layer, helping gradients flow through deep stacks.

**Feed-forward network**  
Two linear layers with a non-linearity applied to each token; holds much of the model's knowledge.

**Encoder-only (BERT)**  
Sees the whole input in both directions. Good for classification, NER and embeddings.

**Decoder-only (GPT, Llama, Claude)**  
Predicts the next token with a causal mask. Good for generation.

**Encoder-decoder (T5, original Transformer)**  
Encoder reads the input, decoder generates output with cross-attention. Good for translation and summarisation.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. BERT vs GPT?**  
BERT is bidirectional and trained with masked tokens, for understanding. GPT is left-to-right, trained on next-token prediction, for generation.

**Q2. What is cross-attention?**  
Decoder queries attend to encoder keys and values, linking output to input.

**Q3. Why residual connections?**  
They make deep networks trainable by giving gradients a direct path.

**Q4. Which architecture for sentiment classification?**  
Encoder-only, like a fine-tuned BERT, or an embedding model plus a classifier.

---

## Part 3: Out-loud check (15 min)

> Say which architecture suits classification vs generation, and why.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Block: attention → add&norm → FFN → add&norm
- Residuals keep gradients flowing
- Encoder (BERT) = understand
- Decoder (GPT) = generate
- Encoder-decoder (T5) = transform text
