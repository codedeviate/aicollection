# Binary Tree

A binary tree is a tree data structure in which each node has at most two children, referred to as the left child and the right child. Binary trees are used in various applications, such as searching, sorting, and representing hierarchical data.

## Key Properties of Binary Trees

1. **Node Structure**: Each node contains a value, a reference to the left child, and a reference to the right child.
2. **Root Node**: The topmost node in the tree.
3. **Leaf Nodes**: Nodes that do not have any children.
4. **Height**: The length of the longest path from the root to a leaf.
5. **Depth**: The length of the path from the root to a given node.

## Types of Binary Trees

1. **Full Binary Tree**: Every node has 0 or 2 children.
2. **Complete Binary Tree**: All levels are completely filled except possibly the last level, which is filled from left to right.
3. **Perfect Binary Tree**: All internal nodes have two children, and all leaf nodes are at the same level.
4. **Balanced Binary Tree**: The height of the left and right subtrees of any node differ by at most one.
5. **Binary Search Tree (BST)**: A binary tree in which the left child contains only nodes with values less than the parent node, and the right child contains only nodes with values greater than the parent node.

## Operations

### Insertion

To insert a value into a binary search tree (BST):
1. Start at the root node.
2. Compare the value to be inserted with the value of the current node.
3. If the value is less than the current node, move to the left child.
4. If the value is greater than the current node, move to the right child.
5. Repeat steps 2-4 until an appropriate empty spot is found.
6. Insert the new node at the empty spot.

### Deletion

To delete a value from a BST:
1. Find the node to be deleted.
2. If the node has no children, simply remove it.
3. If the node has one child, replace the node with its child.
4. If the node has two children, find the in-order successor (smallest value in the right subtree) or in-order predecessor (largest value in the left subtree), replace the node's value with the successor's or predecessor's value, and delete the successor or predecessor.

### Search

To search for a value in a BST:
1. Start at the root node.
2. Compare the value to be searched with the value of the current node.
3. If the value is equal to the current node, return the node.
4. If the value is less than the current node, move to the left child.
5. If the value is greater than the current node, move to the right child.
6. Repeat steps 2-5 until the value is found or the search reaches a leaf node.

## Example

Here is an example of a binary search tree implementation in Python:

```python
class TreeNode:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.val = key

class BinarySearchTree:
    def __init__(self):
        self.root = None

    def insert(self, key):
        if self.root is None:
            self.root = TreeNode(key)
        else:
            self._insert(self.root, key)

    def _insert(self, node, key):
        if key < node.val:
            if node.left is None:
                node.left = TreeNode(key)
            else:
                self._insert(node.left, key)
        else:
            if node.right is None:
                node.right = TreeNode(key)
            else:
                self._insert(node.right, key)

    def search(self, key):
        return self._search(self.root, key)

    def _search(self, node, key):
        if node is None or node.val == key:
            return node
        if key < node.val:
            return self._search(node.left, key)
        return self._search(node.right, key)

    def delete(self, key):
        self.root = self._delete(self.root, key)

    def _delete(self, node, key):
        if node is None:
            return node
        if key < node.val:
            node.left = self._delete(node.left, key)
        elif key > node.val:
            node.right = self._delete(node.right, key)
        else:
            if node.left is None:
                return node.right
            elif node.right is None:
                return node.left
            temp = self._min_value_node(node.right)
            node.val = temp.val
            node.right = self._delete(node.right, temp.val)
        return node

    def _min_value_node(self, node):
        current = node
        while current.left is not None:
            current = current.left
        return current

# Example usage
bst = BinarySearchTree()
bst.insert(10)
bst.insert(5)
bst.insert(15)
bst.insert(2)
bst.insert(7)

print(bst.search(7))  # Output: <__main__.TreeNode object at ...>
bst.delete(10)
print(bst.search(10))  # Output: None
```

This example demonstrates the basic operations of a binary search tree, including insertion, deletion, and search.