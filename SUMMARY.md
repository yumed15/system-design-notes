# Table of contents

* [The Art of Scalable Systems: Designing for Success](README.md)

## BASICS

* [Key Characteristics of Distributed Systems](basics/key-characteristics-of-distributed-systems.md)
* [DNS](basics/dns.md)
* [Load Balancer](basics/load-balancer.md)
* [API Gateway](basics/api-gateway.md)
* [Caching](basics/caching.md)
* [Message Queues](basics/message-queues.md)
* [Proxies](basics/proxies.md)
* [Databases](basics/databases.md)
* [ACID](basics/acid.md)
* [CAP Theorem](basics/cap-theorem.md)
* [PACEL Theorem](basics/pacel-theorem.md)

## System Design patterns

* [Bloom filters](system-design-patterns/bloom-filters.md)
* [Consistent hashing](system-design-patterns/consistent-hashing.md)
* [Quorum/Consensus](system-design-patterns/quorum-consensus.md)
* [Leader and Follower](system-design-patterns/leader-and-follower.md)
* [Write-ahead Log](system-design-patterns/write-ahead-log.md)
* [Segmented Log](system-design-patterns/segmented-log.md)
* [High-Water Mark](system-design-patterns/high-water-mark.md)
* [Locking Lease](system-design-patterns/locking-lease.md)
* [Checksum](system-design-patterns/checksum.md)
* [Vector Clocks](system-design-patterns/vector-clocks.md)
* [Liveness](system-design-patterns/liveness/README.md)
  * [Heartbeat](system-design-patterns/liveness/heartbeat.md)
  * [Gossip Protocol](system-design-patterns/liveness/gossip-protocol.md)
  * [Phi Accrual Failure Detection](system-design-patterns/liveness/phi-accrual-failure-detection.md)
* [Split Brain with Generation Clock](system-design-patterns/split-brain-with-generation-clock.md)
* [Split Brain with Fencing](system-design-patterns/split-brain-with-fencing.md)
* [Resyncing Nodes](system-design-patterns/resyncing-nodes/README.md)
  * [Read Repair](system-design-patterns/resyncing-nodes/read-repair.md)
  * [Merkle trees](system-design-patterns/resyncing-nodes/merkle-trees.md)
  * [Hinted Handoff](system-design-patterns/resyncing-nodes/hinted-handoff.md)

## DATA SYNCHRONISATION PATTERNS

* [Two-phase commit (2pc) Pattern](data-synchronisation-patterns/cqrs.md)
* [CQRS](data-synchronisation-patterns/two-phase-commit.md)
* [Saga](data-synchronisation-patterns/saga.md)
* [Transactional outbox](data-synchronisation-patterns/transactional-outbox.md)
* [Change Data Capture (CDC)](data-synchronisation-patterns/change-data-capture-cdc.md)

## Monolith Decomposition Patterns

* [Monolith vs Microservices](monolith-decomposition-patterns/monolith-vs-microservices.md)
* [Motivation](monolith-decomposition-patterns/motivation.md)
* [The Strangler Fig Migration Pattern](monolith-decomposition-patterns/the-strangler-fig-migration-pattern.md)
* [Domain-Driven Design](monolith-decomposition-patterns/domain-driven-design.md)
* [Other Approaches](monolith-decomposition-patterns/other-approaches.md)

## REAL WORLD SCENARIOS

* [System Design Interview Template](real-world-scenarios/system-design-interview-template.md)
* [Design a Distributed Message Queue & Event Streaming Platform](real-world-scenarios/untitled.md)

## 💰 Payments Services

* [Parties: Acquirer, Issuer](payments-services/parties-acquirer-issuer.md)
* [Events: Chargebacks, Reversals](payments-services/events-chargebacks-reversals.md)

## 🛣 Infrastructure

* [K8S - ClusterIP vs NodePort vs LoadBalancer](infrastructure/k8s-clusterip-vs-nodeport-vs-loadbalancer.md)
