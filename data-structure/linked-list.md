# 链表

## 双向链表、循环链表

## 题目

### [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

```golang
func reverseList(head *ListNode) *ListNode {
    var preNode *ListNode = nil
    var curNode *ListNode = head

    for curNode != nil {
        curNode.Next, preNode, curNode = preNode, curNode, curNode.Next
    }

    return preNode
}
```

### [两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs)

```golang
func swapPairs(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }

    newHead := head.Next
    head.Next = swapPairs(newHead.Next)
    newHead.Next = head
    return newHead
}
```

### [判断链表中是否有环](https://leetcode-cn.com/problems/linked-list-cycle)

方法1：遍历链表，存入set结构，判断如果出现重复，则有环。

方法2：快慢指针，慢指针走一步，快指针走两步，如果有环总会相遇

```golang
func hasCycle(head *ListNode) bool {
    if head == nil || head.Next == nil {
        return false
    }

    slow, fast := head, head.Next
    for fast.Next != nil && fast.Next.Next != nil {
        if slow == fast {
            return true
        }

        slow = slow.Next
        fast = fast.Next.Next
    } 

    return false
}
```

### [判断链表中是否有环，如果环，返回入环的第一个节点](https://leetcode-cn.com/problems/linked-list-cycle-ii)

方法1：遍历链表，存入set结构，判断如果出现重复，则有环，返回节点

```golang
func detectCycle(head *ListNode) *ListNode {
    listMap := map[*ListNode]struct{}{}
    for head != nil {
        if _, ok := listMap[head]; ok {
            return head
        }

        listMap[head] = struct{}{}
        head = head.Next
    }

    return nil
}
```

### [K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)