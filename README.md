# AI/ML Engineer Interview Prep: 50 Days

A day-by-day study plan for entry-level Software Developer, ML Engineer and AI Engineer (RAG) interviews.

## How each day works (about 2 hours)

1. **45 min coding:** try the problem for 25 minutes, then read the approach and re-code it yourself.
2. **60 min concepts:** read the scenario and concepts, answer the interview questions out loud.
3. **15 min check:** answer the day's check without notes. Only then tick it off.

Each day's page ends with a short review block for quick revision.

**Tracking progress:** when you finish a day, change its ⬜ in the **Done** column to ✅. Only tick it once you can answer the **Check** question out loud without notes.

## Main plan

| Done | Day | Topic | Coding problem | Concepts to learn | Check |
|:---:|---|---|---|---|---|
| ⬜ | 1 | [ML Workflow and Data Leakage](01-ml-foundations/day-01-ml-workflow-and-data-leakage.md) | Encode and Decode Strings | **ML workflow:** problem framing, train/val/test split, data leakage, baselines | Leakage example |
| ⬜ | 2 | [Linear Regression and Gradient Descent](01-ml-foundations/day-02-linear-regression-and-gradient-descent.md) | Contains Duplicate | **Linear regression:** MSE loss, gradient descent, learning rate, batch vs mini-batch | Explain GD |
| ⬜ | 3 | [Logistic Regression and Softmax](01-ml-foundations/day-03-logistic-regression-and-softmax.md) | Valid Anagram | **Logistic regression:** sigmoid, log loss, decision boundary, softmax for multi-class | Why log loss? |
| ⬜ | 4 | [Bias, Variance and Regularisation](01-ml-foundations/day-04-bias-variance-and-regularisation.md) | Group Anagrams | **Generalisation:** bias vs variance, under/overfitting, L1 vs L2, early stopping | Fix overfitting |
| ⬜ | 5 | [Classification Metrics](01-ml-foundations/day-05-classification-metrics.md) | Top K Frequent Elements | **Classification metrics:** confusion matrix, precision, recall, F1, ROC-AUC vs PR-AUC, thresholds | Metric for fraud? |
| ⬜ | 6 | [Regression Metrics, Cross-Validation and Tuning](01-ml-foundations/day-06-regression-metrics-cross-validation-and-tuning.md) | Product of Array Except Self | **Validation:** MAE, RMSE, R²; k-fold, stratified, time-series split; grid vs random search | Pick a split |
| ⬜ | 7 | [Decision Trees, Random Forests and Boosting](01-ml-foundations/day-07-decision-trees-random-forests-and-boosting.md) | Longest Consecutive Sequence | **Trees:** Gini/entropy, depth; random forest (bagging); gradient boosting, XGBoost | Bagging vs boosting |
| ⬜ | 8 | [Feature Engineering and Imbalanced Data](01-ml-foundations/day-08-feature-engineering-and-imbalanced-data.md) | Subarray Sum Equals K | **Features:** scaling, one-hot vs target encoding, missing values, class weights, SMOTE | 3 imbalance fixes |
| ⬜ | 9 | [Unsupervised Learning: K-Means and PCA](01-ml-foundations/day-09-unsupervised-learning-k-means-and-pca.md) | Valid Sudoku | **Unsupervised:** k-means, elbow method, PCA, explained variance | PCA simply |
| ⬜ | 10 | [Neural Network Fundamentals](01-ml-foundations/day-10-neural-network-fundamentals.md) | Valid Palindrome | **Neural nets:** activations (ReLU, sigmoid, softmax), forward pass, backprop, vanishing gradients | Why ReLU? |
| ⬜ | 11 | [Training Deep Networks](01-ml-foundations/day-11-training-deep-networks.md) | 3Sum | **Training:** SGD, momentum, Adam, LR schedules, weight init, batch norm, dropout | Role of dropout |
| ⬜ | 12 | [SQL Part 1: Core Queries](02-sql/day-12-sql-part-1-core-queries.md) | Container With Most Water | **SQL 1:** SELECT/WHERE, INNER/LEFT/SELF joins, GROUP BY + HAVING, NULL handling | Join types |
| ⬜ | 13 | [SQL Part 2: Advanced Queries](02-sql/day-13-sql-part-2-advanced-queries.md) | Best Time to Buy and Sell Stock | **SQL 2:** subqueries, CTEs, window functions (ROW_NUMBER, RANK, LAG, running SUM), indexes | Top 3 per group |
| ⬜ | 14 | [CNNs, RNNs and Why Transformers Won](03-transformers-and-llms/day-14-cnns-rnns-and-why-transformers-won.md) | Longest Substring Without Repeating Characters | **Sequence models:** CNN basics, RNN/LSTM, why transformers replaced RNNs | RNN limits |
| ⬜ | 15 | [Tokenisation and Embeddings](03-transformers-and-llms/day-15-tokenisation-and-embeddings.md) | Longest Repeating Character Replacement | **Text to vectors:** tokenisation (BPE, WordPiece), embeddings, cosine similarity | Why close vectors? |
| ⬜ | 16 | [Attention and Self-Attention](03-transformers-and-llms/day-16-attention-and-self-attention.md) | Valid Parentheses | **Attention:** Q, K, V, scaled dot-product, multi-head, positional encoding, causal mask | Attention in 2 min |
| ⬜ | 17 | [Transformer Architecture](03-transformers-and-llms/day-17-transformer-architecture.md) | Min Stack | **Transformer block:** residuals, layer norm, FFN; BERT vs GPT vs T5 | Which for what? |
| ⬜ | 18 | [How LLMs Are Trained](03-transformers-and-llms/day-18-how-llms-are-trained.md) | Daily Temperatures | **LLM training:** pretraining, SFT, RLHF vs DPO, context window, scaling | SFT vs RLHF |
| ⬜ | 19 | [Decoding and Inference Basics](03-transformers-and-llms/day-19-decoding-and-inference-basics.md) | Binary Search | **Decoding:** greedy, beam search, temperature, top-k, top-p, KV cache | Temperature |
| ⬜ | 20 | [Prompting vs RAG vs Fine-Tuning](03-transformers-and-llms/day-20-prompting-vs-rag-vs-fine-tuning.md) | Search in Rotated Sorted Array | **Adapting LLMs:** prompting vs RAG vs fine-tuning, LoRA, QLoRA, PEFT | FAQ bot choice |
| ⬜ | 21 | [Prompt Engineering](03-transformers-and-llms/day-21-prompt-engineering.md) | Find Minimum in Rotated Sorted Array | **Prompting:** system prompts, few-shot, chain-of-thought, JSON output, prompt injection | Fix a vague prompt |
| ⬜ | 22 | [The RAG Pipeline End to End](04-rag-evals-agents/day-22-the-rag-pipeline-end-to-end.md) | Reverse Linked List | **RAG pipeline:** ingest, parse, chunk, embed, index, retrieve, augment, generate | Draw RAG |
| ⬜ | 23 | [Chunking Strategies](04-rag-evals-agents/day-23-chunking-strategies.md) | Merge Two Sorted Lists | **Chunking:** fixed, recursive, semantic, structure-aware; size, overlap, metadata | Chunk size trade-off |
| ⬜ | 24 | [Vector Databases and Similarity Search](04-rag-evals-agents/day-24-vector-databases-and-similarity-search.md) | Linked List Cycle | **Vector DBs:** FAISS, Chroma, pgvector, Pinecone; cosine vs dot vs L2; ANN, HNSW, IVF | Why ANN? |
| ⬜ | 25 | [Improving Retrieval](04-rag-evals-agents/day-25-improving-retrieval.md) | Remove Nth Node From End of List | **Better retrieval:** BM25, hybrid search, RRF, cross-encoder reranking, query rewriting, HyDE | Fix bad retrieval |
| ⬜ | 26 | [LLM Evals Part 1: Building an Eval Set](04-rag-evals-agents/day-26-llm-evals-part-1-building-an-eval-set.md) | LRU Cache | **LLM evals 1:** golden datasets, exact match, BLEU/ROUGE limits, LLM-as-judge, human review | Build an eval set |
| ⬜ | 27 | [LLM Evals Part 2: Evaluating RAG](04-rag-evals-agents/day-27-llm-evals-part-2-evaluating-rag.md) | Invert Binary Tree | **LLM evals 2 (RAG):** recall@k, MRR, faithfulness, answer relevance, context precision, RAGAS, regression tests | Is RAG good? |
| ⬜ | 28 | [Hallucination and Guardrails](04-rag-evals-agents/day-28-hallucination-and-guardrails.md) | Maximum Depth of Binary Tree | **Hallucination:** causes, grounding, citations, abstaining, guardrails, output validation | 3 fixes |
| ⬜ | 29 | [Agents and Tool Calling](04-rag-evals-agents/day-29-agents-and-tool-calling.md) | Same Tree | **Agents:** tool calling, ReAct loop, planning, stop conditions, tool error handling | How tools are picked |
| ⬜ | 30 | [Agent Design: Memory, Multi-Agent and Human-in-the-Loop](04-rag-evals-agents/day-30-agent-design-memory-multi-agent-and-human-in-the-l.md) | Binary Tree Level Order Traversal | **Agent design:** short/long-term memory, multi-agent, LangGraph state, human-in-the-loop, MCP | When multi-agent? |
| ⬜ | 31 | [LLM Latency](04-rag-evals-agents/day-31-llm-latency.md) | Validate Binary Search Tree | **Latency:** TTFT vs throughput, streaming, batching, KV cache, quantisation (INT8/4), semantic cache | Cut latency |
| ⬜ | 32 | [LLM Cost and Observability](04-rag-evals-agents/day-32-llm-cost-and-observability.md) | Lowest Common Ancestor of a BST | **Cost + observability:** tokens, prompt caching, model routing, context trimming, tracing (LangSmith) | Cut cost |
| ⬜ | 33 | [APIs and FastAPI](05-engineering-and-mlops/day-33-apis-and-fastapi.md) | Kth Largest Element in an Array | **APIs:** REST verbs, status codes, FastAPI, Pydantic validation, async/await, SSE streaming | Request lifecycle |
| ⬜ | 34 | [Docker Part 1: Images and Containers](05-engineering-and-mlops/day-34-docker-part-1-images-and-containers.md) | Merge K Sorted Lists | **Docker 1:** image vs container, Dockerfile, layers & caching, build/run, ports, volumes, env vars | Image vs container |
| ⬜ | 35 | [Docker Part 2: Production Images and Compose](05-engineering-and-mlops/day-35-docker-part-2-production-images-and-compose.md) | Number of Islands | **Docker 2:** multi-stage builds, slim images, docker-compose, registries, secrets | Why compose? |
| ⬜ | 36 | [CI/CD Pipelines](05-engineering-and-mlops/day-36-ci-cd-pipelines.md) | Clone Graph | **CI/CD:** Git branches & PRs, pytest, GitHub Actions: lint → test → build → deploy, staging vs prod | Draw a pipeline |
| ⬜ | 37 | [MLOps: Tracking, Versioning and Drift](05-engineering-and-mlops/day-37-mlops-tracking-versioning-and-drift.md) | Course Schedule | **MLOps:** MLflow tracking, model registry, data/model versioning, monitoring, data vs concept drift, retraining | Drift types |
| ⬜ | 38 | [System Design Framework](06-system-design/day-38-system-design-framework.md) | Rotting Oranges | **Design framework:** functional & non-functional reqs, estimates, API, high-level, deep dive, trade-offs | Recite steps |
| ⬜ | 39 | [Scaling Basics: Load Balancing, Caching, CDN](06-system-design/day-39-scaling-basics-load-balancing-caching-cdn.md) | Subsets | **Scaling:** vertical vs horizontal, load balancing, stateless services, Redis cache (TTL, LRU), CDN | Cache placement |
| ⬜ | 40 | [The Data Layer: SQL vs NoSQL, Replication, Sharding](06-system-design/day-40-the-data-layer-sql-vs-nosql-replication-sharding.md) | Combination Sum | **Data layer:** SQL vs NoSQL, indexing, replication, sharding, consistency, CAP theorem | CAP example |
| ⬜ | 41 | [Async Systems: Queues, Retries and Rate Limiting](06-system-design/day-41-async-systems-queues-retries-and-rate-limiting.md) | Word Search | **Async systems:** Kafka/SQS, pub/sub, workers, retries, idempotency, rate limiting (token bucket) | Why a queue? |
| ⬜ | 42 | [Design: URL Shortener](06-system-design/day-42-design-url-shortener.md) | Climbing Stairs | **Design:** URL shortener (ID generation, redirects, caching, analytics) | 30 min on paper |
| ⬜ | 43 | [Design: Chat and Notification System](06-system-design/day-43-design-chat-and-notification-system.md) | House Robber | **Design:** chat / notification system (WebSockets, fan-out, delivery guarantees) | 1M users online |
| ⬜ | 44 | [ML Design: Recommendation System](06-system-design/day-44-ml-design-recommendation-system.md) | Coin Change | **ML design:** recommender (candidate gen, ranking, features, offline/online metrics, A/B tests) | A/B test plan |
| ⬜ | 45 | [ML Design: Model Serving at Scale](06-system-design/day-45-ml-design-model-serving-at-scale.md) | Longest Increasing Subsequence | **ML design:** model serving (batch vs real-time, autoscaling, GPUs, canary rollout, monitoring) | Batch vs real-time |
| ⬜ | 46 | [AI Design: Enterprise RAG Chatbot](06-system-design/day-46-ai-design-enterprise-rag-chatbot.md) | Word Break | **AI design:** enterprise RAG chatbot (access control, doc freshness, evals, cost, latency) | Hourly doc updates |
| ⬜ | 47 | [AI Design: Customer-Support Agent](06-system-design/day-47-ai-design-customer-support-agent.md) | Unique Paths | **AI design:** support agent (tools, guardrails, escalation to human, logging, evals) | Stop unsafe actions |
| ⬜ | 48 | [Debugging Mindset](07-debugging-and-behavioural/day-48-debugging-mindset.md) | Maximum Subarray | **Debugging:** reproduce, isolate, hypothesise, test, fix, verify; ML (loss stuck) & RAG (bad context) | RAG wrong: check first |
| ⬜ | 49 | [Working With Coding Agents](07-debugging-and-behavioural/day-49-working-with-coding-agents.md) | Merge Intervals | **Coding agents:** give context + constraints, plan first, review diffs, write tests, verify output | Your workflow |
| ⬜ | 50 | [Behavioural Interviews and STAR](07-debugging-and-behavioural/day-50-behavioural-interviews-and-star.md) | Implement Trie | **Behavioural:** 6 STAR stories (challenge, failure, conflict, leadership, fast learning, impact) | Each under 2 min |

## Bonus topics (Days 51–60)

Do these after Day 50, or use the optional third hour on busy weeks.

| Done | Day | Topic | Coding problem | Concepts to learn | Check |
|:---:|---|---|---|---|---|
| ⬜ | 51 | [Probability and Statistics](08-bonus/day-51-probability-and-statistics.md) | Search a 2D Matrix | **Probability & stats:** distributions, Bayes, CLT, p-values, Type I/II errors | Bayes example |
| ⬜ | 52 | [A/B Testing and Experiments](08-bonus/day-52-a-b-testing-and-experiments.md) | Koko Eating Bananas | **A/B testing:** sample size, power, peeking, guardrail metrics, novelty effect | Design an A/B test |
| ⬜ | 53 | [Linear Algebra and Calculus for ML](08-bonus/day-53-linear-algebra-and-calculus-for-ml.md) | Permutations | **Linear algebra & calculus:** dot product, matrix shapes, eigenvectors/SVD, chain rule | Attention in maths |
| ⬜ | 54 | [Python Deep Dive for Engineers](08-bonus/day-54-python-deep-dive-for-engineers.md) | Generate Parentheses | **Python deep dive:** GIL, asyncio vs threads vs processes, decorators, dataclasses | When asyncio? |
| ⬜ | 55 | [Networking and the Web](08-bonus/day-55-networking-and-the-web.md) | Pacific Atlantic Water Flow | **Networking:** DNS, TCP vs UDP, HTTP/HTTPS, TLS, JWT, CORS | Type a URL: what happens |
| ⬜ | 56 | [Cloud Basics (AWS)](08-bonus/day-56-cloud-basics-aws.md) | Minimum Window Substring | **Cloud (AWS):** EC2/ECS/Lambda, S3, IAM, VPC, Bedrock, SageMaker | Deploy a RAG API |
| ⬜ | 57 | [Kubernetes Basics](08-bonus/day-57-kubernetes-basics.md) | Insert Interval | **Kubernetes:** pods, deployments, services, ingress, HPA, probes | How K8s scales |
| ⬜ | 58 | [Data Pipelines and ETL](08-bonus/day-58-data-pipelines-and-etl.md) | Non-overlapping Intervals | **Data pipelines:** ETL vs ELT, Airflow DAGs, lake vs warehouse, quality checks | Nightly pipeline |
| ⬜ | 59 | [LLM Security and Responsible AI](08-bonus/day-59-llm-security-and-responsible-ai.md) | Decode Ways | **LLM security:** OWASP LLM Top 10, indirect injection, PII, excessive agency | 3 defences |
| ⬜ | 60 | [Multimodal and Vision-Language Models](08-bonus/day-60-multimodal-and-vision-language-models.md) | Longest Common Subsequence | **Multimodal:** ViT, CLIP, vision-language models, multimodal RAG, voice agents | Explain a VLM |

## Resources

- Coding: NeetCode 150 roadmap
- ML: StatQuest videos, Andrew Ng's Machine Learning Specialization
- Transformers: Jay Alammar's "The Illustrated Transformer", Andrej Karpathy's videos
- RAG and agents: LlamaIndex and LangChain docs, DeepLearning.AI short courses
- System design: "Designing Machine Learning Systems" by Chip Huyen, ByteByteGo
# ai-ml-design-concepts
