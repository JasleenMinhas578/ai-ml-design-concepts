# Day 56: BONUS: Cloud Basics (AWS)

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Minimum Window Substring (Sliding window, Hard)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Check every substring for containing all characters: O(n² · k).

**Best approach:** Expand the right pointer until the window has all needed counts, then shrink from the left while still valid, tracking the smallest window.

```python
from collections import Counter

def minWindow(s, t):
    need, missing = Counter(t), len(t)
    left = start = 0
    best = float('inf')
    for right, ch in enumerate(s):
        if need[ch] > 0:
            missing -= 1
        need[ch] -= 1
        while missing == 0:
            if right - left + 1 < best:
                best, start = right - left + 1, left
            need[s[left]] += 1
            if need[s[left]] > 0:
                missing += 1
            left += 1
    return '' if best == float('inf') else s[start:start + best]
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

You deploy your RAG API: the Docker image goes to ECR, runs on ECS Fargate behind a load balancer, PDFs live in S3, a Lambda triggers re-indexing when a file is uploaded, and the LLM is called through Bedrock. Secrets sit in Secrets Manager.

### What to understand

**Compute**  
EC2 (virtual machines), ECS/EKS (containers), Lambda (serverless functions, pay per call).

**Storage**  
S3 (objects/files), EBS (disks), RDS/Aurora (managed SQL), DynamoDB (NoSQL).

**Networking**  
VPC, subnets, security groups, load balancers, API Gateway.

**IAM**  
Users, roles and policies; least privilege for every service.

**ML/AI services**  
SageMaker (train/deploy models), Bedrock (hosted foundation models), OpenSearch (vector search).

**Serverless vs containers**  
Lambda: no servers, scales to zero, time limits and cold starts. Containers: more control for long-running services.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Lambda vs ECS?**  
Lambda for short, event-driven tasks; ECS for long-running services needing more control.

**Q2. Where would you store uploaded PDFs?**  
S3, with events triggering processing.

**Q3. What is IAM least privilege?**  
Each service gets only the permissions it needs.

**Q4. How would you deploy an ML API on AWS?**  
Container in ECR → ECS/EKS behind a load balancer, autoscaling, secrets in Secrets Manager, logs in CloudWatch.

---

## Part 3: Out-loud check (15 min)

> Sketch an AWS deployment for a RAG API.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- EC2 / ECS / Lambda
- S3 for files
- IAM least privilege
- Bedrock / SageMaker
- Serverless vs containers trade-off
