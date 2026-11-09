# Day 50: Behavioural Interviews and STAR

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Implement Trie (Trie, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Store words in a list and scan for prefixes: O(n × length) per query.

**Best approach:** Each node has a dict of children and an end-of-word flag. Insert, search and startsWith walk character by character. O(length).

```python
class Trie:
    def __init__(self):
        self.root = {}
    def insert(self, word):
        node = self.root
        for ch in word:
            node = node.setdefault(ch, {})
        node['$'] = True
    def _walk(self, s):
        node = self.root
        for ch in s:
            if ch not in node:
                return None
            node = node[ch]
        return node
    def search(self, word):
        node = self._walk(word)
        return bool(node and '$' in node)
    def startsWith(self, prefix):
        return self._walk(prefix) is not None
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Asked 'Tell me about a time you failed', you describe a RAG demo that broke in front of your team because you hadn't tested on real documents, what you changed (an eval set, testing with real data), and how the next release went smoothly.

### What to understand

**STAR**  
Situation (brief context), Task (your goal), Action (what YOU did, the biggest part), Result (outcome with numbers if possible).

**Six core stories**  
A challenge, a failure, a conflict, leadership/initiative, learning something fast, and your proudest impact.

**Reuse stories**  
One good story can answer several questions; know which fits which.

**Say 'I', not 'we'**  
Interviewers need to know your part.

**Tell me about yourself**  
90 seconds: background → what you've built (internship, projects) → why this role.

**Your questions**  
Prepare 3–4: team, what success looks like in 6 months, how they evaluate their AI systems.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Tell me about a time you failed.**  
Pick a real failure, own it, explain what you learned and what changed after.

**Q2. Tell me about a conflict with a teammate.**  
Focus on understanding their view, the data used to decide, and the respectful outcome.

**Q3. Why this company?**  
Connect their product or problems to your experience and interests specifically.

**Q4. What questions do you have for us?**  
Ask about the team's challenges, how they measure success, and how they ship AI features.

---

## Part 3: Out-loud check (15 min)

> Tell each of your 6 STAR stories in under 2 minutes.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- S-T-A-R, most time on Action
- 6 stories cover most questions
- 'I' not 'we'
- Results with numbers
- Always have questions ready
