# Bloom filters

### Motivation

When you have a large set of structured data (identified by record IDs) stored in a set of data files, what is the most efficient way to know which file might contain our required data?

Reading each file would be slow as we have to read a lot of data from the disk.

We could build an index on each data file and store it in a separate index file. Each index file will be sorted on the record ID. If we want to search an ID in this index, the best we can do is a Binary Search.

### Solution

A Bloom filter is a **probabilistic** **data structure** based on **hashing** designed to tell you, **rapidly** and **memory-efficiently**, **whether an element is present in a set.** Elements are not added to the set but their hash is.

The price paid for this efficiency is that a Bloom filter is a **probabilistic data structure**: it tells us that the element either _**definitely is not**_** ** in the set or _**may be**_** ** in the set, thus **false positives** are possible.

**How does it work?**

* &#x20;An empty Bloom filter is a bit-array of `m` bits, all set to 0. We also have `k` different hash functions, each of which maps a set element to one of the `m` bit positions.
* To add an element, feed it to the hash functions to get `k` bit positions, and set the bits at these positions to 1.
* To test if an element is in the set, feed it to the hash functions to get `k` bit positions.
  * If any of the bits at these positions is 0, the element is **definitely not** in the set.
  * If all are 1, then the element **may be** in the set.

<figure><img src="../.gitbook/assets/Diana Playground (1).jpg" alt=""><figcaption></figcaption></figure>

**Choosing Hash Functions**

The hash functions used in a Bloom filter should be [**independent**](http://en.wiktionary.org/wiki/independent\_function) and [**uniformly distributed**](http://en.wikipedia.org/wiki/Uniform\_distribution\_\(discrete\)). Some examples of independent enough include [murmur](https://sites.google.com/site/murmurhash/), [xxHash](https://github.com/Cyan4973/xxHash), the [fnv](http://isthe.com/chongo/tech/comp/fnv/) series of hashes, and [HashMix](https://web.archive.org/web/20061030103559/http://www.concentric.net/\~Ttwang/tech/inthash.htm).\
The more hash functions you have, the slower your bloom filter, and the quicker it fills up. If you have too few, however, you may suffer too many false positives.

****

**Choosing the length of a Bloom filter**

The false positive rate of you filter can vary on the length of the filter. A larger filter will have less false positives, and a smaller one more.

The rate of the false positives will be approximately $$(1-e^{-kn/m})^k$$ where $$n$$ = number of elements you expect to insert, $$m$$= number of bits in the bloom filter and $$k$$= number of hash functions.

To choose the size of a bloom filter, we:

1. Choose a ballpark value for _n_
2. Choose a value for _m_
3. Calculate the optimal value of _k_
4. Calculate the error rate for our chosen values of _n_, _m_, and _k_. If it's unacceptable, return to step 2 and change m; otherwise we're done.

### Time and Space Complexity

**Time**

If we are using a bloom filter with $$m$$ bits and $$k$$ hash function, insertion and search will both take $$O(k)$$ time. In both cases, we just need to run the input through all of the hash functions. Then we just check the output bits.

| Operation | Complexity |
| :-------: | :--------: |
| insertion |    O(k)    |
|   search  |    O(k)    |

**Space**

To truly understand the space complexity of the bloom filter, you have to first choose your parameters. You could make a bloom filter with $$k=1$$ and it would just be a [hash table](https://brilliant.org/wiki/hash-tables/) that ignores collisions. However, you would have a very large $$m$$ if you wanted to keep your false positive rate low. The space of the actual data structure (what holds the data) is simply $$O(m)$$.

| Space | Complexity |
| :---: | :--------: |
| space |    O(m)    |

### Applications

#### BigTable

In **BigTable** (and Cassandra), any read operation has to read from all SSTables that make up a Tablet. If these SSTables are not in memory, the read operation may end up doing many disk accesses. To reduce the number of disk accesses, BigTable uses Bloom filters.

Bloom filters are created for SSTables (particularly for the locality groups). They help reduce the number of disk accesses by predicting if an SSTable may contain data corresponding to a particular row or column pair. For certain applications, a small amount of Tablet server memory used for storing Bloom filters drastically reduces the number of disk-seeks, thereby improving read performance.



**Resources:**

* [Nice Interactive Bloom Filter](https://llimllib.github.io/bloomfilter-tutorial/)
