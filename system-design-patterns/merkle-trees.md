# Merkle trees

### Motivation

Repairing stale data for nodes that were down and now are back online but the nodes are far behind and a [read repair](read-repair.md) would take too long.

### Solution

Naively splitting up the entire range to calculate checksums for comparison, is not very feasible.

We can use ** **<mark style="background-color:yellow;">**merkle trees**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">= binary tree of hashes, where each internal node is the hash of its two children, and each leaf node is a hash of a portion of the original data</mark>

We can use merkle trees by:

* comparing the root hashes of both trees.
* if they are equal, stop.
* recursively checking the left and right children.

This way the amount of data exchanged is minimized. The principal advantage of a Merkle tree is that each branch of the tree can be checked independently without requiring nodes to download the entire tree or the entire data set.

<figure><img src="../.gitbook/assets/Diana Playground (13).jpg" alt=""><figcaption></figcaption></figure>
