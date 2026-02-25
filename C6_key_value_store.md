# Basics

- Due to performance reasons, short key works better.

Question: What do you mean by value is an opaque object in a key value store?
Question: What do you mean by tunable consistency?

# Single server key-value store
- implement using a hash table
- Optimize for space using:
    - data compression
    - keeping frequwntly used data in memory & rest on disk
- But Even with optimisation, a single server KV store can reach the ceiling very quickly, and that's why we need a distributed KV store.

# CAP Theorem

Question: Though I understand easily what CAP means individually, give me an example and explain to me all three of them in more detail, specifically the partition tolerance part. What is it? Also, we were talking about partition tolerance of data, but what is network tolerance? I just have no idea about it.

- we know that one of them "Needs to go blud!"
-  Since network failure is unavoidable, a distributed system must tolerate network partition; thus, a CA system cannot exist. 
- Therefore, we only have two options remaining: CP and AP systems: 

    1. CP (consistency and partition tolerance) systems: a CP key-value store supports consistency and partition tolerance while sacrificing availability.
    2. AP (availability and partition tolerance) systems: an AP key-value store supports availability and partition tolerance while sacrificing consistency.

# Data partition & Data replication
- consistent hashing
- With virtual nodes, the first N nodes on the ring may be owned by fewer than N physical servers. To avoid this issue, we only choose unique servers while performing the clockwise walk logic.


# Consistency

Didn't really understand what NWR mean.

### Consistency Models

- Strong, weak, and eventual
- We are suggested to use, and also would tend to prefer eventual consistency in our Kiwi store designing, which is similar to what DynamoDB and Cassandra use. --> In such case the client can get inconsistent values and **IS FORCED TO RECONCILE**.

# Inconsistency resolution: versioning

Did not understand anything about version clocks.

# Handling Failures

### Failure Detection
- All-to-all Multicasting
- Gossip Protocol

### Handling Temporary Failures

Question: What is the strict quorum approach?
Question: What is sloppy quorum?
Question: What is hinted handoff?
Question: Why in this diagram 6-10, we choose s3 and not s1 and s2?


### Handling Permanent Failures

- Anti Entropy protocol --> Implemented using a Merkle tree


Question: I understood how the Merkle tree is built and how, based on the hashes, we can understand and locate which bin has an inconsistency issue, but what is the anti entropy protocol? Building a Merkle tree and using its hashes to find and locate the inconsistency, is this anti entropy protocol all together?

### Handling data center outage

Need to replicate data across data centers - Vanilla shit!

# System Architecture Diagram

Tasks are:
1. Handle client API
6. Storage engine
5. Replication
3. Conflict resolution
2. Failure detection
4. Failure repair mechanism

Question: is something like coordinator present in DynamoDB and Cassandra architectures?

# Write Path
1. We write the request details in a commit log file.
2. Data is saved in the memory cache.
3. Whenever the memory cache is full or reaches a predefined threshold, we flush all of data to SSTables


# Read Path
1. We check the memory cache. If it's there, we get it because that will be a cache hit || else it's a cache miss.
2. If it's a miss, then we use the bloom filter to check in the SSTables.
3. We get the actual location where the data might be on SSTables.
4. We get resultant data from SSTables and we return it to the client.
