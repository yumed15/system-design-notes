# System Design Interview Template

**REQUIREMENTS \[5 min]**

1. Functional and non-functional requirements
2. Use cases and scenarios that will not be covered
3. Who are the users
4. What is the expected load
5. Usage patterns

**ESTIMATIONS \[5 min]**

1. Traffic estimates - throughout (QPS), latency
2. Read/Write ratio
3. Storage estimates
4. Memory estimates

**DESIGN GOALS \[5 min]**

1. CP vs AP - weak/eventual/strong consistency

**HIGH LEVEL DESIGN \[5-10min]**

1. Basic system components
2. Database schema
3. API design
4. Use cases flows

**DEEP DIVE \[15-20min]**

1. Scalability and Performance Optimisations
   1. Caching - CDN, cache invalidation, cache eviction policies, expiration policies
   2. API Gateway
   3. Proxies
   4. Databases - SQL vs NoSQL, sharding
   5. Async Processing - message queues, event driven architecture, FSMs, transactional outbox, change data capture, cqrs, saga, 2 phase commit
2. Fault Tolerance and Redundancy
   1. Leader and follower - quorum/consensus
   2. Liveness - heartbeat, gossip protocol, phi accrual failure detection
   3. Resyncing nodes - hinted handoff, merkle trees, read repair
   4. Nodes coming back up - split brain with fencing, split brain with generation clock
   5. WAL
3. Logging, Monitoring, Observability&#x20;
   1. Metrics to track&#x20;
   2. Alerts to set up
4. Deployment Strategies
   1. Rolling, blue/green, canary, A/B testing, shadow release
5. Examples of cloud technologies that might be used for the system
