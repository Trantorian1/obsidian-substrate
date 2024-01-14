> 📚 A **Merkle tree** is a [tree](https://en.wikipedia.org/wiki/Tree_(data_structure) "Tree (data structure)") in which every leaf [node](https://en.wikipedia.org/wiki/Tree_(data_structure)#Terminology "Tree (data structure)") contains the [cryptographic hash](https://en.wikipedia.org/wiki/Cryptographic_hash_function "Cryptographic hash function") of a data block. Every node that is not a leaf contains a cryptographic hash of the contents of its child nodes. This is applied recursively until the root node of the tree, called **merkle node**.

*[wikipedia](https://en.wikipedia.org/wiki/Merkle_tree)*

# Data authenticity

Due to the way in which the hash of the *merkle node* is computed, this guarantees that any change in state, at *any* point in the merkle tree, will result in a change in the hash at the *merkle node*. Therefore, it is only necessary to verify the hash at the *merkle root* of the tree to verify the authenticity of it's data.

> ℹ️ Note that due to the way in which it is created, each inner node in a Merkle tree is itself a Merkle root. This means that, starting at the top-most Merkle root, if any discrepancy in a hash is found, it is easy to find the source of these discrepancies by comparing the hashes of recursively smaller Merkle trees.

---
# Traversal

While bottom-to-top traversal in a Merkle tree is trivial, consisting in the recursive hashing of child nodes until a single root node is reached, top-to-bottom traversal is less straightforwards.

> 📚 A **Merkle path** is a top-to-bottom traversal path in a Merkle tree, specifying how to reach a value from the merkle root.

While Merkle trees maintain the structure of binary trees, they do not however maintain the advantages of their binary ordering of data: since only the leaf nodes contain any actual data, and all other nodes only contain hashes, it is impossible to retrieve a leaf value through a dichotomic search along it's path. It is therefore necessary to know the path, or *merkle path*, to a value in advance in order to retrieve it.

> ⚠️ it should be clear by now that Merkle trees are optimized for guaranteeing data authenticity, not data retrieval. The advantages of binary and Merkle trees might be combined by having a balanced binary trees store the merkle paths to each value in the merkle tree for faster lookup while maintaining properties of data authenticity, though this will still be done at the cost of performance compared to traditional hashmaps. Another solution is to use [transparent hashing algorithms](https://docs.substrate.io/build/runtime-storage/#transparent-hashing-algorithms) in such a way that the merkle path to a value might be reverse-engineered during top-to-bottom traversal.

---
# Storing data

Since Merkle trees only store hashes, identifying data such as string keys need to combined as part of the hash. This is typically done by reserving a part of the hash (for example the first 128 bits) to store the key or any other identifier, while the rest of the hash stores the actual value being queried.