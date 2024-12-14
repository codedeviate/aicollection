# Linked list

A linked list is a linear data structure where each element (node) contains a value and a reference (link) to the next node in the sequence. Linked lists are dynamic and can grow or shrink in size by allocating or deallocating memory as needed.

## Key Properties of Linked Lists

1. **Node Structure**: Each node contains a value and a reference to the next node.
2. **Head**: The first node in the linked list.
3. **Tail**: The last node in the linked list, which points to `null` (or `None` in Python).
4. **Dynamic Size**: The size of the linked list can change dynamically.

## Types of Linked Lists

1. **Singly Linked List**: Each node points to the next node.
2. **Doubly Linked List**: Each node points to both the next and the previous node.
3. **Circular Linked List**: The last node points back to the first node, forming a circle.

## Operations

### Insertion

To insert a value into a singly linked list:
1. Create a new node with the given value.
2. If inserting at the head, set the new node's next reference to the current head and update the head to the new node.
3. If inserting at the tail, traverse the list to find the last node, set its next reference to the new node, and update the tail to the new node.
4. If inserting at a specific position, traverse the list to find the node before the desired position, set the new node's next reference to the next node, and update the previous node's next reference to the new node.

### Deletion

To delete a value from a singly linked list:
1. If deleting the head, update the head to the next node.
2. If deleting the tail, traverse the list to find the second-to-last node, set its next reference to `null`, and update the tail to this node.
3. If deleting a node at a specific position, traverse the list to find the node before the desired position, update its next reference to skip the node to be deleted.

### Search

To search for a value in a singly linked list:
1. Start at the head node.
2. Traverse the list, comparing each node's value with the target value.
3. If the value is found, return the node.
4. If the value is not found and the end of the list is reached, return `null`.

## Example

Here is an example of a singly linked list implementation in Python:

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None

    def insert_at_head(self, value):
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node

    def insert_at_tail(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            return
        last = self.head
        while last.next:
            last = last.next
        last.next = new_node

    def delete_value(self, value):
        current = self.head
        if current and current.value == value:
            self.head = current.next
            current = None
            return
        prev = None
        while current and current.value != value:
            prev = current
            current = current.next
        if current is None:
            return
        prev.next = current.next
        current = None

    def search(self, value):
        current = self.head
        while current:
            if current.value == value:
                return current
            current = current.next
        return None

# Example usage
linked_list = SinglyLinkedList()
linked_list.insert_at_head(10)
linked_list.insert_at_tail(20)
linked_list.insert_at_tail(30)

print(linked_list.search(20))  # Output: <__main__.Node object at ...>
linked_list.delete_value(20)
print(linked_list.search(20))  # Output: None
```

This example demonstrates the basic operations of a singly linked list, including insertion, deletion, and search.