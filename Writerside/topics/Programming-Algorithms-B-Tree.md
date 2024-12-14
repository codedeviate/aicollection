# B+ Tree

A B+ tree is an extension of a B-tree that maintains sorted data and allows for efficient insertion, deletion, and search operations. It is commonly used in databases and file systems. The main difference between B-trees and B+ trees is that in B+ trees, all data is stored in the leaf nodes, and internal nodes only store keys to guide the search.

## Key Properties of B+ Trees

1. **Balanced Tree**: All leaf nodes are at the same depth.
2. **Node Structure**: Internal nodes contain only keys and child pointers, while leaf nodes contain keys and data pointers.
3. **Order**: The maximum number of children a node can have is defined by the order `m` of the B+ tree.
4. **Key Constraints**:
    - Each internal node can have at most `m-1` keys.
    - Each internal node (except the root) must have at least `ceil(m/2) - 1` keys.
5. **Children Constraints**:
    - Each internal node can have at most `m` children.
    - Each internal node (except the root) must have at least `ceil(m/2)` children.
6. **Leaf Nodes**: Leaf nodes are linked together to allow for efficient range queries.

## Operations

### Search

To search for a key in a B+ tree:
1. Start at the root node.
2. Perform a binary search within the internal node to find the range of keys.
3. If the key is found in an internal node, continue to the appropriate child node.
4. If the key is found in a leaf node, return the data.
5. If the key is not found, the key does not exist.

### Insertion

To insert a key into a B+ tree:
1. Find the appropriate leaf node where the key should be inserted.
2. Insert the key into the leaf node in sorted order.
3. If the leaf node overflows (i.e., it has `m` keys), split the node:
    - Create a new leaf node and move the median key to the parent.
    - Distribute the remaining keys between the two leaf nodes.
4. If the parent node overflows, recursively split the parent.

### Deletion

To delete a key from a B+ tree:
1. Find the leaf node containing the key.
2. Remove the key from the leaf node.
3. If the leaf node underflows (i.e., it has fewer than `ceil(m/2) - 1` keys), rebalance the tree by borrowing a key from a sibling or merging with a sibling.
4. If an internal node underflows, recursively rebalance the tree.

## Example

Consider a B+ tree of order 3 (each node can have at most 2 keys and 3 children).

### Initial Tree

```
       [10]
      /    \
   [5]     [15, 20]
```

### Insertion of 25

1. Insert 25 into the appropriate leaf node.
2. The node [15, 20] overflows, so split it:
    - Move 20 to the parent.
    - Create a new leaf node [25].

```
       [10, 20]
      /    |    \
   [5]   [15]  [25]
```

### Deletion of 10

1. Find 10 in the root node.
2. Replace 10 with its successor (15).
3. Delete 15 from the leaf node.

```
       [15, 20]
      /    |    \
   [5]   []   [25]
```

This example illustrates the basic operations of a B+ tree, including insertion and deletion, while maintaining balance and order.