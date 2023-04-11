# Split Brain with Generation Clock

### Motivation

Existence of <mark style="background-color:yellow;">**zombie leaders**</mark> (leader node that had been deemed dead by the system and has since come back online). Another node has taken its place, but the zombie leader might not know that yet and now the system now has two active leaders that could be issuing conflicting commands.

<mark style="background-color:yellow;">**Split Brain**</mark> = scenario in which a distributed system has two or more active leaders

### Solution

Solved through the use of <mark style="background-color:yellow;">**Generation Clock**</mark>, which is simply a monotonically increasing number to indicate a server’s generation.

* every time a new leader is elected, the generation number gets incremented: if the old leader had a generation number of ‘1’, the new one will have ‘2’.
* the generation number is included in every request that is sent from the leader to other nodes.
* nodes can now easily differentiate the real leader by simply trusting the leader with the highest number.
* the generation number should be persisted on disk, so that it remains available after a server reboot. (e.g. be written with every request in the WAL)

<figure><img src="../.gitbook/assets/Diana Playground (10).jpg" alt=""><figcaption></figcaption></figure>

### Applications

**Kafka**: To handle Split-brain (where we could have multiple active controller brokers), Kafka uses ‘**Epoch number**,’ which is simply a monotonically increasing number to indicate a server’s generation.

\
