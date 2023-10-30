# The Art of Scalable Systems: Designing for Success

Buckle up, intrepid coder! The Art of Scalable Systems is your passport to unraveling the mysteries of services. Explore the hilarious mishaps and ingenious solutions to everyday problems.

📚 NB: This is an attempt at documenting all my system design notes from reading and hands-on experience, starting with explaining the basic components of a service to providing examples of real world systems and discussing tradeoffs of possible solutions.

## Table of contents

#### Basic Concepts

| System components                          | System concepts                          |
| ------------------------------------------ | ---------------------------------------- |
| [Load Balancer](basics/load-balancer.md)   | [ACID](basics/acid.md)                   |
| [API Gateway](basics/api-gateway.md)       | [CAP Theorem](basics/cap-theorem.md)     |
| [Caching](basics/caching.md)               | [PACEL Theorem](basics/pacel-theorem.md) |
| [DNS](basics/dns.md)                       |                                          |
| [Message Queues](basics/message-queues.md) |                                          |
| [Proxies](basics/proxies.md)               |                                          |
| [Databases](basics/databases.md)           |                                          |

#### Design Patterns

| Problem                            | Solution                                                                                                                                                                                                                                                                        |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Check set contains                 | [Bloom Filters](system-design-patterns/bloom-filters.md)                                                                                                                                                                                                                        |
| Where to insert data               | [Consistent Hashing](system-design-patterns/consistent-hashing.md)                                                                                                                                                                                                              |
| Ensure strong consistency          | [Quorum Consensus](system-design-patterns/quorum-consensus.md)                                                                                                                                                                                                                  |
| Ensure high availability           | [Leader And Follower](system-design-patterns/leader-and-follower.md)                                                                                                                                                                                                            |
| Atomicity in data transfers        | <p><a href="system-design-patterns/write-ahead-log.md">Write Ahead Log</a><br><a href="system-design-patterns/segmented-log.md">Segmented Log</a><br><a href="system-design-patterns/high-water-mark.md">High Water Mark</a></p>                                                |
| Concurrent updates to file         | [Locking Lease](system-design-patterns/locking-lease.md)                                                                                                                                                                                                                        |
| Concurrent node writes             | [Vector Clocks](system-design-patterns/vector-clocks.md)                                                                                                                                                                                                                        |
| Node liveness                      | <p><a href="system-design-patterns/liveness/heartbeat.md">Heartbeat</a><br><a href="system-design-patterns/liveness/gossip-protocol.md">Gossip Protocol</a><br><a href="system-design-patterns/liveness/phi-accrual-failure-detection.md">Phi Accrual Failure Detection</a></p> |
| Deal with dead nodes coming back   | <p><a href="system-design-patterns/split-brain-with-fencing.md">Split Brain With Fencing</a><br><a href="system-design-patterns/split-brain-with-generation-clock.md">Split Brain With Generation Clock</a></p>                                                                 |
| Update dead nodes with missed data | [Hinted Handoff](system-design-patterns/resyncing-nodes/hinted-handoff.md)                                                                                                                                                                                                      |
| Update stale nodes                 | <p><a href="system-design-patterns/resyncing-nodes/read-repair.md">Read Repair</a><br><a href="system-design-patterns/resyncing-nodes/merkle-trees.md">Merkle Trees</a></p>                                                                                                     |
| Check data inconsistency           | [Checksum](system-design-patterns/checksum.md)                                                                                                                                                                                                                                  |

#### Data Synchronisation Patterns

| Chapters                                                                              |
| ------------------------------------------------------------------------------------- |
| [CQRS](data-synchronisation-patterns/two-phase-commit.md)                             |
| [Two Phase Commit](data-synchronisation-patterns/cqrs.md)                             |
| [Transactional Outbox](data-synchronisation-patterns/transactional-outbox.md)         |
| [Change Data Capture (CDC)](data-synchronisation-patterns/change-data-capture-cdc.md) |

#### Monolith Decomposition Patterns

| Chapters                                                                                                      |
| ------------------------------------------------------------------------------------------------------------- |
| [Domain Driven Design](monolith-decomposition-patterns/domain-driven-design.md)                               |
| [The Strangler Fig Migration Pattern](monolith-decomposition-patterns/the-strangler-fig-migration-pattern.md) |

#### Real World Scenarios

| Chapters                                                                                 |
| ---------------------------------------------------------------------------------------- |
| [Distributed Message Queue & Event Streaming Platform](real-world-scenarios/untitled.md) |

**Infrastructure Bits and Bobs**

| Chapters                                                                                                   |
| ---------------------------------------------------------------------------------------------------------- |
| [K8S - ClusterIP vs NodePort vs LoadBalancer](infrastructure/k8s-clusterip-vs-nodeport-vs-loadbalancer.md) |

#### Payments Domain

| Chapters                                                                            |
| ----------------------------------------------------------------------------------- |
| [Parties: Acquirer, Issuer](payments-services/parties-acquirer-issuer.md)           |
| [Events: Chargebacks, Reversals](payments-services/events-chargebacks-reversals.md) |
