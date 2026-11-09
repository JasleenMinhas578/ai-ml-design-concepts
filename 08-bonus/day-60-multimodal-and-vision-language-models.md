# Day 60: BONUS: Multimodal and Vision-Language Models

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Longest Common Subsequence (2D DP, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try every subsequence of one string: exponential.

**Best approach:** dp[i][j] = dp[i−1][j−1] + 1 if characters match, else max(dp[i−1][j], dp[i][j−1]). O(m × n).

```python
def longestCommonSubsequence(a, b):
    dp = [[0] * (len(b) + 1) for _ in range(len(a) + 1)]
    for i in range(1, len(a) + 1):
        for j in range(1, len(b) + 1):
            if a[i-1] == b[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    return dp[-1][-1]
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

An insurer's claims bot receives car-damage photos and scanned forms. A vision-language model reads the form fields and describes the damage; scanned PDFs with charts are indexed using page images, so RAG can answer questions about tables and diagrams.

### What to understand

**Vision Transformer (ViT)**  
Splits an image into patches, embeds each like a token, and runs a transformer.

**CLIP**  
Trains image and text encoders so matching pairs have similar embeddings; enables text-to-image search.

**Vision-language models**  
An image encoder connected to an LLM so it can answer questions about images.

**Multimodal RAG**  
Index images, tables and page screenshots, not just text; use OCR or VLM descriptions.

**Document AI**  
OCR, layout detection and table extraction for PDFs and forms.

**Speech**  
Speech-to-text (Whisper) and text-to-speech enable voice agents.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How does a model 'see' an image?**  
Patches become embeddings processed by a transformer, then aligned with text.

**Q2. What is CLIP used for?**  
Matching images and text in a shared embedding space: search, zero-shot classification.

**Q3. How would you build RAG over PDFs with charts?**  
Extract text and tables, describe or embed page images, and store them with page metadata.

**Q4. How would you build a voice agent?**  
Speech-to-text → LLM with tools → text-to-speech, streaming each stage for low latency.

---

## Part 3: Out-loud check (15 min)

> Explain how a vision-language model works and multimodal RAG.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- ViT = image patches as tokens
- CLIP = shared image-text space
- VLM = image encoder + LLM
- Multimodal RAG: index images/tables
- Voice = STT → LLM → TTS
