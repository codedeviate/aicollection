# Combined Linked List and BTree

To combine a doubly linked list and a B-tree into the same class in Go, we need to define a single structure that incorporates both data structures. Below is the implementation:

### Doubly Linked List Node

```go
package main

type DllNode struct {
    key  int
    prev *DllNode
    next *DllNode
}
```

### B-tree Node

```go
package main

type BTreeNode struct {
    keys     []int
    children []*BTreeNode
    isLeaf   bool
    dllNode  *DllNode
}
```

### Combined Data Structure

```go
package main

type CombinedDataStructure struct {
    head *DllNode
    tail *DllNode
    root *BTreeNode
    t    int // Minimum degree
}

func NewCombinedDataStructure(t int) *CombinedDataStructure {
    return &CombinedDataStructure{t: t}
}

func (cds *CombinedDataStructure) Insert(key int) {
    newNode := &DllNode{key: key}
    if cds.head == nil {
        cds.head = newNode
        cds.tail = newNode
    } else {
        cds.tail.next = newNode
        newNode.prev = cds.tail
        cds.tail = newNode
    }

    if cds.root == nil {
        cds.root = &BTreeNode{isLeaf: true, keys: []int{key}, dllNode: newNode}
    } else {
        if len(cds.root.keys) == 2*cds.t-1 {
            newRoot := &BTreeNode{children: []*BTreeNode{cds.root}}
            cds.splitChild(newRoot, 0)
            cds.root = newRoot
        }
        cds.insertNonFull(cds.root, key, newNode)
    }
}

func (cds *CombinedDataStructure) splitChild(parent *BTreeNode, i int) {
    t := cds.t
    y := parent.children[i]
    z := &BTreeNode{isLeaf: y.isLeaf, keys: append([]int(nil), y.keys[t:]...)}
    parent.keys = append(parent.keys[:i], append([]int{y.keys[t-1]}, parent.keys[i:]...)...)
    parent.children = append(parent.children[:i+1], append([]*BTreeNode{z}, parent.children[i+1:]...)...)
    y.keys = y.keys[:t-1]
    if !y.isLeaf {
        z.children = append([]*BTreeNode(nil), y.children[t:]...)
        y.children = y.children[:t]
    }
}

func (cds *CombinedDataStructure) insertNonFull(node *BTreeNode, key int, dllNode *DllNode) {
    i := len(node.keys) - 1
    if node.isLeaf {
        node.keys = append(node.keys, 0)
        for i >= 0 && key < node.keys[i] {
            node.keys[i+1] = node.keys[i]
            i--
        }
        node.keys[i+1] = key
        node.dllNode = dllNode
    } else {
        for i >= 0 && key < node.keys[i] {
            i--
        }
        i++
        if len(node.children[i].keys) == 2*cds.t-1 {
            cds.splitChild(node, i)
            if key > node.keys[i] {
                i++
            }
        }
        cds.insertNonFull(node.children[i], key, dllNode)
    }
}
```

### Main Function

```go
package main

import "fmt"

func main() {
    cds := NewCombinedDataStructure(3)

    cds.Insert(10)
    cds.Insert(20)
    cds.Insert(5)
    cds.Insert(6)
    cds.Insert(12)
    cds.Insert(30)
    cds.Insert(7)
    cds.Insert(17)

    // Print Doubly Linked List
    current := cds.head
    for current != nil {
        fmt.Printf("%d ", current.key)
        current = current.next
    }
}
```

This code defines a combined data structure that includes both a doubly linked list and a B-tree, with methods to insert elements into both data structures. The `main` function demonstrates how to use this combined structure.