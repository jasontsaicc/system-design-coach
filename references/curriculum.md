# System Design Interview Curriculum

> Target: Big tech SD interviews (FAANG, AWS, Google, etc.)
> Pace: ~1 hour/day, deep learning over memorization
> Approach: Discussion → PoC → Notes → Reflect

---

## Phase 0: Thinking Framework (Day 1-3)

### Day 1: What SD Interviews Actually Test
- The 4 scoring dimensions: Problem Navigation, Design, Technical Depth, Trade-offs
- Analyze good vs bad answers for the same question
- **Discussion**: Deconstruct a real SD interview rubric

### Day 2: Back-of-Envelope Estimation
- Powers of 2, latency numbers every engineer should know
- Practice: Estimate YouTube daily storage, Twitter QPS
- **Exercise**: Build an estimation cheat sheet you actually understand

### Day 3: Your SD Answer Framework (4-Step Method)
- Step 1: Clarify requirements & scope (functional + non-functional)
- Step 2: High-level design (API + data model + architecture)
- Step 3: Deep dive into core components
- Step 4: Scale, trade-offs, monitoring
- Time budget for 45-min SD interview:
  - [0-5 min] Clarify requirements (DO NOT SKIP)
  - [5-10 min] Back-of-envelope estimation (if needed)
  - [10-20 min] High-level design
  - [20-35 min] Deep dive into 1-2 core components
  - [35-45 min] Scale, trade-offs, monitoring
- Standard Whiteboard Diagram Template — the 8-block skeleton (see `8-block-skeleton.md`)
- Practice: Answer "Design URL Shortener" using the framework (dry run)

---

## Phase 1: Core Building Blocks (Day 4-16)

> Apply the **Observability Mini** to every topic:
> SLIs → SLO target → Alerts → Dashboards

### Day 4-5: Load Balancer & Reverse Proxy
- DNS fundamentals — resolution flow, TTL, record types
- DNS-based load balancing (weighted, latency-based, failover)
- L4 vs L7 load balancing — when to use which
- Algorithms: Round Robin, Least Connections, IP Hash, Weighted
- Health checks, sticky sessions, connection draining
- **DevOps**: ALB vs NLB, target group health checks
- **PoC**: Nginx L4/L7 LB with Docker Compose

### Day 6-7: Caching & CDN Strategies
- Cache levels: Browser → CDN → App → DB
- Patterns: Cache-Aside, Write-Through, Write-Behind, Read-Through
- Eviction: LRU, LFU, TTL
- Cache invalidation — the hard problem
- CDN: Edge caching, Pull vs Push, cache invalidation strategies
- **DevOps**: ElastiCache cluster mode, CloudFront behaviors, cache hit ratio
- **PoC**: Redis cache layer, measure latency with/without cache

### Day 8-9: Database Selection
- SQL vs NoSQL vs NewSQL — decision framework
- Indexing: B-tree (read-optimized) vs LSM-tree (write-optimized)
- Denormalization, sharding intro, connection pooling
- WAL, read replicas, consistency trade-offs
- **Data Model Design Template**: Entities → Access patterns → Partition key → Secondary index → Hot partition risk → Backfill strategy
- **PoC**: Same problem with SQL vs NoSQL, compare trade-offs

### Day 10-11: Message Queue & Async Processing
- Why async? Decoupling, buffering, peak handling
- SQS vs Kafka vs RabbitMQ — positioning
- Delivery semantics: at-least-once, at-most-once, exactly-once
- Dead letter queue, retry strategies
- **DevOps**: SQS FIFO vs Standard, DLQ monitoring
- **PoC**: Producer-consumer with failures simulation

### Day 12-13: API Design
- REST vs gRPC vs GraphQL — trade-off matrix
- Pagination: Offset vs Cursor
- Versioning strategies, idempotency
- **PoC**: Design & implement a small API

### Day 14: Security & Authentication
- JWT vs Session-based authentication
- OAuth 2.0 flow basics
- API Key management, HTTPS, encryption
- **DevOps**: Cognito, OIDC integration, secrets rotation

### Day 15-16: Consistent Hashing & Data Partitioning
- Why simple hash mod N fails
- Consistent hashing with virtual nodes
- Range-based vs Hash-based partitioning
- **PoC**: Implement consistent hashing from scratch

### Checkpoint: Mini-Mock (Day 16)
> 15-minute drill: Explain any building block using the 4-step framework.

---

## Phase 2: Distributed Systems Core (Day 17-26)

### Day 17-18: CAP Theorem in Practice
- CAP is about network partitions, not a daily choice
- Real-world examples: DynamoDB (AP), Zookeeper (CP)
- PACELC model as a more practical framework

### Day 19-20: Consistency Models
- Strong, Eventual, Causal, Read-your-writes
- Quorum: W + R > N
- Vector clocks, conflict resolution
- **PoC**: Simulate eventual consistency

### Day 21-22: Replication & Leader Election
- Single-leader, multi-leader, leaderless
- Raft consensus algorithm (simplified)
- Service Discovery: Consul, Kubernetes DNS, Cloud Map

### Day 23-24: Rate Limiting & Circuit Breaker
- Token Bucket, Sliding Window, Fixed Window
- Circuit Breaker pattern (Closed → Open → Half-Open)
- Bulkhead pattern
- **PoC**: Token Bucket + Circuit Breaker implementation

### Distributed Systems Kill Pack (Reference)
- **Idempotency Key**: scope, TTL, storage, behavior
- **Deduplication**: message ID, dedup window, consumer vs infra side
- **Distributed Lock**: lease-based, fencing token, failure modes

### Day 25: Observability Consolidation
- Metrics, Logs, Traces — three pillars
- Distributed tracing, SLI/SLO/SLA formalization
- Structured logging, correlation IDs
- How to discuss monitoring in SD interviews

### Day 26: Bloom Filter, Gossip Protocol & Advanced Concepts
- Bloom Filter: probabilistic membership testing
- Gossip Protocol: node discovery and state sharing
- Distributed Transactions overview (2PC/3PC)

### Checkpoint: Mid-Mock (Day 26)
> 30-minute mock: Design a distributed key-value store.

---

## Phase 3: Classic SD Problems (Day 27-53)

> Format: Day 1 = Discussion & Design | Day 2 = PoC + Diagram + Notes
> Complex problems get 3 days.

### Tier 1: Must Do (Day 27-45)

| Days | Problem | Key Concepts | Difficulty |
|------|---------|-------------|-----------|
| 27-28 | URL Shortener | Hashing, base62, read-heavy | ★★☆ |
| 29-30 | Unique ID Generator | Snowflake, clock sync, coordination-free | ★★☆ |
| 31-32 | Distributed Rate Limiter | Distributed sliding window, Redis Lua, race conditions | ★★★ |
| 33-34 | Notification System | Push/Pull, priority queue, multi-channel | ★★★ |
| 35-37 | Chat System | WebSocket, presence, read receipts, group chat | ★★★★ |
| 38-39 | Distributed Cache | Consistent hashing, invalidation at scale, thundering herd | ★★★ |
| 40-42 | News Feed | Fan-out on write/read, ranking, celebrity problem | ★★★★ |
| 43-45 | Payment System | Idempotency, SAGA, exactly-once, reconciliation | ★★★★ |

### Tier 2: Should Do (Day 46-53)

| Days | Problem | Key Concepts |
|------|---------|-------------|
| 46-47 | Metrics & Logging System | Time-series DB, aggregation, sampling |
| 48-49 | Search Autocomplete | Trie, ranking, Elasticsearch |
| 50-51 | Web Crawler | BFS/DFS, URL frontier, dedup (Bloom filter) |
| 52-53 | Proximity Service | Geohash, QuadTree, spatial indexing |

### Tier 3: Nice to Have (Optional)

Video Streaming, Cloud Storage, Distributed Task Scheduler, Ticket/Booking System — concepts already covered by Tier 1/2.

---

## Phase 4: Advanced & Mock Interviews (Day 54-61)

### Day 54-55: Trade-off Analysis Deep Dive
- Practice specific trade-off scenarios (5 min each)
- Trap & Pivot Drills — practice graceful pivots when initial design hits a wall
- Cost estimation for designs

### Day 56-57: Mock Interview Round 1
- 45-minute strictly timed mock interview
- Detailed feedback on 4 dimensions
- Practice thinking aloud, following interviewer hints

### Day 58-59: Weak Spot Reinforcement
- Review all notes, identify patterns in mistakes
- Re-do 2-3 difficult designs
- Practice articulating trade-offs in 2-3 sentences

### Day 60-61: Final Mock Interview (Brutal Mode)
- 2 back-to-back 45-min interviews
- Interviewer interrupts, changes requirements, challenges aggressively
- Double trap drills — chaining pivots without losing composure

---

## PoC Language & Tools

- **Default PoC Language**: Go (chosen for concurrency model and interview relevance)
  - Students can use any language they're comfortable with
- **Diagrams**: Mermaid + whiteboard practice
- **Infrastructure**: Docker Compose for local PoC environments
- **Notes**: Markdown

---

## Daily Routine Summary

```
A. [5 min]   Review — Check yesterday's notes + mistakes
B. [3 min]   Introduction — Analogy/scenario for today's concept
C. [12 min]  Core Teaching — Feynman + Simon method
D. [20 min]  Hands-On — PoC or design exercise
E. [5 min]   Simon Drill — Self recall + AI challenge
F. [10-15 min] Interview Drill — Mini SD mock with 4-step framework
G. [5 min]   Notes — Using notes template
H. [5 min]   Progress — Update tracking + preview tomorrow
    Total ≈ 65-70 min
```
