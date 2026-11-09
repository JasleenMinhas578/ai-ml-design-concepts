# Day 46: AI Design: Enterprise RAG Chatbot

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Word Break (DP + hash set, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try every split recursively: exponential.

**Best approach:** dp[i] = True if s[:i] can be segmented. For each i, check j < i with dp[j] True and s[j:i] in the word set.

```python
def wordBreak(s, wordDict):
    words = set(wordDict)
    dp = [True] + [False] * len(s)
    for i in range(1, len(s) + 1):
        for j in range(i):
            if dp[j] and s[j:i] in words:
                dp[i] = True
                break
    return dp[len(s)]
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Design an internal assistant for 10,000 employees over Confluence, Google Drive and Slack. HR documents must only be visible to HR, documents update hourly, and answers need citations within 3 seconds.

### What to understand

**Ingestion pipeline**  
Connectors pull documents; change detection (webhooks or hourly sync) re-chunks and re-embeds only changed files.

**Access control**  
Store each chunk's permissions; filter retrieval by the user's groups so nobody sees what they can't open.

**Retrieval**  
Hybrid search + reranking + metadata filters (source, date, team).

**Generation**  
Prompt with context, citations required, 'I don't know' allowed; stream the answer.

**Latency and cost**  
Cache frequent questions, route simple ones to smaller models, limit context size.

**Evals and monitoring**  
Golden set per department, faithfulness checks, user feedback, tracing and cost dashboards.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How do you handle documents updated hourly?**  
Incremental sync: detect changes, re-embed changed chunks, delete stale ones, keep update timestamps.

**Q2. How do you enforce permissions?**  
Permission metadata on every chunk and filtering by the user's groups at query time.

**Q3. How do you keep latency under 3 seconds?**  
Fast ANN index, small rerank set, streaming, caching and smaller models where possible.

**Q4. How do you measure quality?**  
Retrieval and generation evals on a golden set, plus feedback and sampled human review.

---

## Part 3: Out-loud check (15 min)

> Design the enterprise RAG bot, including 'docs update hourly'.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Connectors + incremental re-embed
- Permission filter on every query
- Hybrid + rerank
- Cite or say 'I don't know'
- Evals, tracing, cost dashboards
