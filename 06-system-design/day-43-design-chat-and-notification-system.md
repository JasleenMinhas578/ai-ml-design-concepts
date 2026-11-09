# Day 43: Design: Chat and Notification System

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** House Robber (DP, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try every subset of non-adjacent houses: exponential.

**Best approach:** At each house: best = max(skip it, rob it + best from two houses back). Keep two variables.

```python
def rob(nums):
    prev, curr = 0, 0
    for n in nums:
        prev, curr = curr, max(curr, prev + n)
    return curr
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Design WhatsApp-style chat for 1 million concurrent users: one-to-one and group messages, online status, delivered/read ticks, and push notifications when offline.

### What to understand

**Real-time connection**  
WebSockets keep a two-way connection open; long polling is a fallback.

**Connection servers**  
Track which server each user is connected to (stored in Redis) so messages are routed correctly.

**Message flow**  
Sender → chat service → store in DB → route to recipient's connection; if offline, push notification and deliver later.

**Storage**  
Wide-column store (Cassandra) partitioned by conversation_id, sorted by time.

**Groups and fan-out**  
Send to each member; for huge groups, fan-out asynchronously via a queue.

**Delivery guarantees**  
Message IDs, acknowledgements, retries and de-duplication for 'sent / delivered / read'.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Why WebSockets?**  
Persistent, low-latency, two-way communication.

**Q2. How do you deliver to an offline user?**  
Store the message, send a push notification, deliver when they reconnect.

**Q3. How do you keep message order?**  
Per-conversation sequence numbers or timestamps from the server.

**Q4. How do you avoid duplicate messages on retries?**  
Client-generated message IDs and de-duplication.

---

## Part 3: Out-loud check (15 min)

> Design chat for 1M online users, covering offline delivery.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- WebSockets for real-time
- Track user → server in Redis
- Store by conversation, time-sorted
- Async fan-out for groups
- IDs + acks + dedupe
