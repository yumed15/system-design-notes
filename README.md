# Welcome

📚 This is an attempt at documenting all my system design notes from reading and on hands experience, starting with explaining the basic components of a service to providing examples of real world problems and how they're currently implemented.

### Table of contents

{% tabs %}
{% tab title="Basic Concepts" %}
| System components                                                                         | System concepts                          |
| ----------------------------------------------------------------------------------------- | ---------------------------------------- |
| [Load Balancer](basics/load-balancer.md)                                                  | [ACID](basics/acid.md)                   |
| [Caching](basics/caching.md)                                                              | [Cap Theorem](basics/cap-theorem.md)     |
| [Message Queues](basics/message-queues.md)                                                | [Pacel Theorem](basics/pacel-theorem.md) |
| [Proxies](basics/proxies.md)                                                              |                                          |
| [Databases](basics/databases.md)                                                          |                                          |
| [DNS](basics/dns.md)                                                                      |                                          |
| [Monolith vs Microservices](monolith-decomposition-patterns/monolith-vs-microservices.md) |                                          |
{% endtab %}

{% tab title="Design Patterns" %}
| Problem                            | Solution                                                                                                                                                                                                                                             |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Check set contains                 | [Bloom Filters](system-design-patterns/bloom-filters.md)                                                                                                                                                                                             |
| Where to insert data               | [Consistent Hashing](system-design-patterns/consistent-hashing.md)                                                                                                                                                                                   |
| Ensure strong consistency          | [Quorum Consensus](system-design-patterns/quorum-consensus.md)                                                                                                                                                                                       |
| Ensure high availability           | [Leader And Follower](system-design-patterns/leader-and-follower.md)                                                                                                                                                                                 |
| Atomicity in data transfers        | <p><a href="system-design-patterns/write-ahead-log.md">Write Ahead Log</a><br><a href="system-design-patterns/segmented-log.md">Segmented Log</a><br><a href="system-design-patterns/high-water-mark.md">High Water Mark</a></p>                     |
| Concurrent updates to file         | [Locking Lease](system-design-patterns/locking-lease.md)                                                                                                                                                                                             |
| Concurrent node writes             | [Vector Clocks](system-design-patterns/vector-clocks.md)                                                                                                                                                                                             |
| Node liveness                      | <p><a href="system-design-patterns/heartbeat.md">Heartbeat</a><br><a href="system-design-patterns/gossip-protocol.md">Gossip Protocol</a><br><a href="system-design-patterns/phi-accrual-failure-detection.md">Phi Accrual Failure Detection</a></p> |
| Deal with dead nodes coming back   | <p><a href="system-design-patterns/split-brain-with-fencing.md">Split Brain With Fencing</a><br><a href="system-design-patterns/split-brain-with-generation-clock.md">Split Brain With Generation Clock</a></p>                                      |
| Update dead nodes with missed data | [Hinted Handoff](system-design-patterns/hinted-handoff.md)                                                                                                                                                                                           |
| Update stale nodes                 | <p><a href="system-design-patterns/read-repair.md">Read Repair</a><br><a href="system-design-patterns/merkle-trees.md">Merkle Trees</a></p>                                                                                                          |
| Check data inconsistency           | [Checksum](system-design-patterns/checksum.md)                                                                                                                                                                                                       |
{% endtab %}

{% tab title="Distributed Data Transactions" %}
|                                    |                                                              |
| ---------------------------------- | ------------------------------------------------------------ |
| Commit or rollback transaction     | [CQRS](distributed-data-design-patterns/two-phase-commit.md) |
| Retrieve data from multiple places | [Two Phase Commit](distributed-data-design-patterns/cqrs.md) |
{% endtab %}

{% tab title="Splitting the monolith" %}
| Chapters                                                                                                      |
| ------------------------------------------------------------------------------------------------------------- |
| [Domain Driven Design](monolith-decomposition-patterns/domain-driven-design.md)                               |
| [The Strangler Fig Migration Pattern](monolith-decomposition-patterns/the-strangler-fig-migration-pattern.md) |
{% endtab %}
{% endtabs %}
