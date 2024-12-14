# Btree

A B-tree is a self-balancing tree data structure that maintains sorted data and allows for efficient insertion, deletion, and search operations. It is commonly used in databases and file systems.

## Key Properties of B-trees

1. **Balanced Tree**: All leaf nodes are at the same depth.
2. **Node Structure**: Each node contains multiple keys and children pointers.
3. **Order**: The maximum number of children a node can have is defined by the order `m` of the B-tree.
4. **Key Constraints**:
    - Each node can have at most `m-1` keys.
    - Each node (except the root) must have at least `ceil(m/2) - 1` keys.
5. **Children Constraints**:
    - Each internal node can have at most `m` children.
    - Each internal node (except the root) must have at least `ceil(m/2)` children.

## Operations

### Search

To search for a key in a B-tree:
1. Start at the root node.
2. Perform a binary search within the node to find the range of keys.
3. If the key is found, return it.
4. If the key is not found and the node is a leaf, the key does not exist.
5. If the key is not found and the node is an internal node, recursively search the appropriate child.

### Insertion

To insert a key into a B-tree:
1. Find the appropriate leaf node where the key should be inserted.
2. Insert the key into the leaf node in sorted order.
3. If the node overflows (i.e., it has `m` keys), split the node:
    - Create a new node and move the median key to the parent.
    - Distribute the remaining keys and children between the two nodes.
4. If the parent node overflows, recursively split the parent.

### Deletion

To delete a key from a B-tree:
1. Find the node containing the key.
2. If the key is in a leaf node, remove it directly.
3. If the key is in an internal node:
    - If the predecessor or successor child has at least `ceil(m/2)` keys, replace the key with the predecessor or successor and delete the key from the child.
    - If both children have fewer than `ceil(m/2)` keys, merge the key and its children.
4. If a node underflows (i.e., it has fewer than `ceil(m/2) - 1` keys), rebalance the tree by borrowing a key from a sibling or merging with a sibling.

## Example

Consider a B-tree of order 3 (each node can have at most 2 keys and 3 children).

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
    - Create a new node [25].

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

This example illustrates the basic operations of a B-tree, including insertion and deletion, while maintaining balance and order.