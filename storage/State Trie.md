> 📚 The Substrate **State trie** is responsible for storing the state of the blockchain in a queryable cached [[Merkle Tree]] (so that common queries are immediately available). This is used to rapidly compare state between blockchain nodes without having to compare the entire node history. [source](https://docs.substrate.io/learn/state-transitions-and-storage/)

# Accessing storage

Storage is accessed via a combination of hashes. This follows different rules depending on the type of storage being queried. See [here](https://docs.substrate.io/learn/state-transitions-and-storage/#querying-storage) for more details.

TODO: https://docs.substrate.io/build/runtime-storage/#transparent-hashing-algorithms