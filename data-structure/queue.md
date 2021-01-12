# 队列

- 队列是一种 先进先出（first in - first out， FIFO）的数据结构，
- 队列中的元素都从后端（rear）入队（push），从前端（front）出队（pop）。

## [用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues/)

使用数组切片；push就是append，pop就是调整切片长度，top就是返回最后一个元素

```golang
type MyStack struct {
    data []int
}

/** Initialize your data structure here. */
func Constructor() MyStack {
    return MyStack{}
}


/** Push element x onto stack. */
func (this *MyStack) Push(x int)  {
    this.data = append(this.data, x)
}


/** Removes the element on top of the stack and returns that element. */
func (this *MyStack) Pop() int {
    if len(this.data) == 0 {
        return 0
    }

    element :=  this.data[len(this.data) - 1]
    this.data = this.data[:len(this.data) - 1]
    return element
}


/** Get the top element. */
func (this *MyStack) Top() int {
    return this.data[len(this.data) - 1]
}


/** Returns whether the stack is empty. */
func (this *MyStack) Empty() bool {
    return len(this.data) == 0
}
```

## [用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

```golang

type MyQueue struct {
    input []int
    output []int
}


/** Initialize your data structure here. */
func Constructor() MyQueue {
    return MyQueue{}
}


/** Push element x to the back of queue. */
func (this *MyQueue) Push(x int)  {
    this.input = append(this.input, x)
}


/** Removes the element from in front of queue and returns that element. */
func (this *MyQueue) Pop() int {
    if len(this.output) > 0 {
        element := this.output[len(this.output) - 1]
        this.output = this.output[:len(this.output) - 1]
        return element
    }

    if len(this.input) == 0 {
        return 0
    }

    for len(this.input) > 0 {
        element := this.input[len(this.input) - 1]
        this.input = this.input[:len(this.input) - 1]

        if len(this.input) == 0 {
            return element
        } else {
            this.output = append(this.output, element)
        }
    }

    return 0
}


/** Get the front element. */
func (this *MyQueue) Peek() int {
    if len(this.output) > 0 {
        return this.output[len(this.output) - 1]
    }

    if len(this.input) == 0 {
        return 0
    }

    for len(this.input) > 0 {
        element := this.input[len(this.input) - 1]
        this.input = this.input[:len(this.input) - 1]
        this.output = append(this.output, element)
    }

    return this.output[len(this.output) - 1]
}


/** Returns whether the queue is empty. */
func (this *MyQueue) Empty() bool {
    return len(this.input) == 0 && len(this.output) == 0
}
```
