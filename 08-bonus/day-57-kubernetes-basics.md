# Day 57: BONUS: Kubernetes Basics

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Insert Interval (Intervals, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Append the new interval and run Merge Intervals: O(n log n).

**Best approach:** One pass: add intervals ending before the new one, merge all overlapping ones, then add the rest. O(n).

```python
def insert(intervals, new):
    res, i = [], 0
    while i < len(intervals) and intervals[i][1] < new[0]:
        res.append(intervals[i]); i += 1
    while i < len(intervals) and intervals[i][0] <= new[1]:
        new = [min(new[0], intervals[i][0]), max(new[1], intervals[i][1])]
        i += 1
    res.append(new)
    return res + intervals[i:]
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Your model API gets 10× traffic every Monday morning. Kubernetes runs it as a Deployment with 3 pods, a Horizontal Pod Autoscaler scales to 20 pods under load, and a rolling update ships new versions without downtime.

### What to understand

**Pod**  
Smallest unit: one or more containers sharing network and storage.

**Deployment**  
Keeps a desired number of pods running; handles rolling updates and rollbacks.

**Service and Ingress**  
Service gives pods a stable address and load-balances; Ingress routes external HTTP traffic.

**ConfigMap and Secret**  
Configuration and sensitive values injected into pods.

**Autoscaling**  
HPA adds pods based on CPU, memory or custom metrics; cluster autoscaler adds nodes.

**Probes and resources**  
Liveness/readiness probes check health; requests/limits reserve CPU, memory and GPUs.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Pod vs Deployment?**  
A pod runs containers; a Deployment manages many pods and their updates.

**Q2. How does Kubernetes scale an API?**  
HPA increases pod count based on metrics.

**Q3. Readiness vs liveness probe?**  
Readiness: ready for traffic? Liveness: should it be restarted?

**Q4. Why not just use Docker on one server?**  
No automatic scaling, healing or zero-downtime rollouts.

---

## Part 3: Out-loud check (15 min)

> Explain how Kubernetes keeps an API running and scales it.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Pod → Deployment → Service
- Ingress for external traffic
- HPA autoscaling
- Readiness vs liveness
- ConfigMap, Secret, resource limits
