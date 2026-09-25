# Odd Even Linked List

## Problem

Given the head of a singly linked list, rearrange the list so that all nodes at **odd indices** come first, followed by all nodes at **even indices**.

The first node is considered to have an odd index, the second node an even index, and so on.

The relative order of nodes within both the odd and even groups must remain the same.

### Example

**Input:**

```text
1 → 2 → 3 → 4 → 5
```

**Output:**

```text
1 → 3 → 5 → 2 → 4
```

## Approach

We use two pointers:

* `odd` → points to the current odd-indexed node.
* `even` → points to the current even-indexed node.
* `evenHead` → stores the beginning of the even-indexed list.

We rearrange the links so that odd-indexed nodes form one list and even-indexed nodes form another list.

Finally, we connect the end of the odd list to the beginning of the even list.

### Steps

1. Check if the list has 0 or 1 node.
2. Set `odd` to the first node and `even` to the second node.
3. Save the first even node using `evenHead`.
4. Connect each odd node to the next odd node.
5. Connect each even node to the next even node.
6. Attach the even list after the odd list.
7. Return the original `head`.

## Code

```cpp
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {

        if (head == NULL || head->next == NULL) {
            return head;
        }

        ListNode* odd = head;
        ListNode* even = head->next;

        ListNode* evenHead = even;

        while (even != NULL && even->next != NULL) {

            odd->next = even->next;
            odd = odd->next;

            even->next = odd->next;
            even = even->next;
        }

        odd->next = evenHead;

        return head;
    }
};
```

## Example Walkthrough

For:

```text
1 → 2 → 3 → 4 → 5
```

Odd-indexed nodes:

```text
1 → 3 → 5
```

Even-indexed nodes:

```text
2 → 4
```

Finally:

```text
1 → 3 → 5 → 2 → 4
```

## Complexity

### Time Complexity: O(n)

We traverse the linked list once. Therefore, the time complexity is **O(n)**, where `n` is the number of nodes.

### Space Complexity: O(1)

We only use a few pointers (`odd`, `even`, and `evenHead`) and do not create any extra array or linked list. Therefore, the extra space complexity is **O(1)**.

## Key Concept

The main idea is:

```text
Separate Odd Nodes
        ↓
Separate Even Nodes
        ↓
Connect Odd List + Even List
```

This solution rearranges the existing links without creating new nodes.
