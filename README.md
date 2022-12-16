---
layout: landing
---

# 📚 Welcome

📚 This is an attempt at documenting all my system design notes from reading and on hands experience, starting with explaining the basic components of a service to providing examples of real world problems and how they're currently implemented.



## Table of contents

{% tabs %}
{% tab title="Basic Concepts" %}
| System components                                                                                      | System concepts                                       |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| [load-balancer.md](basics/load-balancer.md "mention")                                                  | [acid.md](basics/acid.md "mention")                   |
| [caching.md](basics/caching.md "mention")                                                              | [cap-theorem.md](basics/cap-theorem.md "mention")     |
| [message-queues.md](basics/message-queues.md "mention")                                                | [pacel-theorem.md](basics/pacel-theorem.md "mention") |
| [proxies.md](basics/proxies.md "mention")                                                              |                                                       |
| [databases.md](basics/databases.md "mention")                                                          |                                                       |
| [dns.md](basics/dns.md "mention")                                                                      |                                                       |
| [monolith-vs-microservices.md](monolith-decomposition-patterns/monolith-vs-microservices.md "mention") |                                                       |
{% endtab %}

{% tab title="Design Patterns" %}
| Problem                            | Solution                                                                                                                                                                                                                                                                                             |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Check set contains                 | [bloom-filters.md](system-design-patterns/bloom-filters.md "mention")                                                                                                                                                                                                                                |
| Where to insert data               | [consistent-hashing.md](system-design-patterns/consistent-hashing.md "mention")                                                                                                                                                                                                                      |
| Ensure strong consistency          | [quorum-consensus.md](system-design-patterns/quorum-consensus.md "mention")                                                                                                                                                                                                                          |
| Ensure high availability           | [leader-and-follower.md](system-design-patterns/leader-and-follower.md "mention")                                                                                                                                                                                                                    |
| Atomicity in data transfers        | <p><a data-mention href="system-design-patterns/write-ahead-log.md">write-ahead-log.md</a><br><a data-mention href="system-design-patterns/segmented-log.md">segmented-log.md</a><br><a data-mention href="system-design-patterns/high-water-mark.md">high-water-mark.md</a></p>                     |
| Concurrent updates to file         | [locking-lease.md](system-design-patterns/locking-lease.md "mention")                                                                                                                                                                                                                                |
| Concurrent node writes             | [vector-clocks.md](system-design-patterns/vector-clocks.md "mention")                                                                                                                                                                                                                                |
| Node liveness                      | <p><a data-mention href="system-design-patterns/heartbeat.md">heartbeat.md</a><br><a data-mention href="system-design-patterns/gossip-protocol.md">gossip-protocol.md</a><br><a data-mention href="system-design-patterns/phi-accrual-failure-detection.md">phi-accrual-failure-detection.md</a></p> |
| Deal with dead nodes coming back   | <p><a data-mention href="system-design-patterns/split-brain-with-fencing.md">split-brain-with-fencing.md</a><br><a data-mention href="system-design-patterns/split-brain-with-generation-clock.md">split-brain-with-generation-clock.md</a></p>                                                      |
| Update dead nodes with missed data | [hinted-handoff.md](system-design-patterns/hinted-handoff.md "mention")                                                                                                                                                                                                                              |
| Update stale nodes                 | <p><a data-mention href="system-design-patterns/read-repair.md">read-repair.md</a><br><a data-mention href="system-design-patterns/merkle-trees.md">merkle-trees.md</a></p>                                                                                                                          |
| Check data inconsistency           | [checksum.md](system-design-patterns/checksum.md "mention")                                                                                                                                                                                                                                          |
{% endtab %}

{% tab title="Distributed Data Transactions" %}
|                                    |                                                                                       |
| ---------------------------------- | ------------------------------------------------------------------------------------- |
| Commit or rollback transaction     | [cqrs.md](distributed-data-design-patterns/cqrs.md "mention")                         |
| Retrieve data from multiple places | [two-phase-commit.md](distributed-data-design-patterns/two-phase-commit.md "mention") |
|                                    |                                                                                       |
{% endtab %}

{% tab title="Splitting the monolith" %}
| Chapters                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------- |
| [domain-driven-design.md](monolith-decomposition-patterns/domain-driven-design.md "mention")                               |
| [the-strangler-fig-migration-pattern.md](monolith-decomposition-patterns/the-strangler-fig-migration-pattern.md "mention") |
|                                                                                                                            |
{% endtab %}
{% endtabs %}
