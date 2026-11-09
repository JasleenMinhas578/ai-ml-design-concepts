# Day 58: BONUS: Data Pipelines and ETL

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Non-overlapping Intervals (Greedy, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try removing every subset: exponential.

**Best approach:** Sort by end time; keep an interval if it starts after the last kept end, otherwise remove it. Count removals.

```python
def eraseOverlapIntervals(intervals):
    intervals.sort(key=lambda x: x[1])
    end, removed = float('-inf'), 0
    for s, e in intervals:
        if s >= end:
            end = e
        else:
            removed += 1
    return removed
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Each night, an Airflow job pulls new support tickets, cleans and de-duplicates them, computes embeddings, and loads them into the vector store. Data-quality checks stop the run if half the tickets have empty text.

### What to understand

**ETL vs ELT**  
Extract-Transform-Load transforms before the warehouse; ELT loads raw data first and transforms inside it (dbt).

**Batch vs streaming**  
Batch processes on a schedule (Airflow, Spark); streaming processes events continuously (Kafka, Flink).

**Orchestration**  
Airflow, Prefect or Dagster run steps as a DAG with retries, schedules and alerts.

**Storage layers**  
Data lake (raw files in S3), warehouse (Snowflake, BigQuery), lakehouse (Delta, Iceberg).

**Data quality**  
Schema checks, null and duplicate checks, ranges (Great Expectations); fail fast on bad data.

**Idempotent pipelines**  
Re-running a job gives the same result; makes backfills and retries safe.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. ETL vs ELT?**  
ETL transforms before loading; ELT loads raw then transforms in the warehouse.

**Q2. How do you keep a RAG index up to date?**  
A scheduled or event-driven pipeline that re-embeds changed documents, with quality checks.

**Q3. Why should pipelines be idempotent?**  
So retries and backfills don't create duplicates.

**Q4. Batch vs streaming?**  
Batch for periodic, high-volume jobs; streaming when freshness matters.

---

## Part 3: Out-loud check (15 min)

> Design a nightly pipeline feeding a vector store.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- ETL vs ELT
- Airflow DAGs with retries
- Lake vs warehouse
- Quality checks fail fast
- Idempotent jobs
