# LRU

- LFU - least frequently used（最近最不常⽤⻚⾯置换算法）
- LRU - least recently usd（最近最少使⽤⻚⾯置换算法）

LRU本质上是一种缓存数据淘汰策略。计算机的缓存容量是有限的，如果缓存满了，就要删除一部分数据，来存放新的数据，那么删除哪些数据？LRU的全程是least recently usd，将那些最近最少使用的数据删除。

## LRU算法数据结构

LRU 缓存算法的核⼼数据结构就是哈希表与双向链表，如下图：

![lru](./images/lru-data-structure.png)

借助哈希表我们可以很快的查找数据，而双向链表实现了数据的优先级，插入数据会将数据插入到链表头部，数据被访问后也会被调整到链表头部，如果数据满了，优先从链表尾部进行数据删除。

## [LRU 缓存机制](https://leetcode-cn.com/problems/lru-cache/#/)

```golang
type  LRUCache struct {
    size int
    capacity int
    cache map[int]*DLinkedNode 
    head *DLinkedNode 
    tail *DLinkedNode 
}

type DLinkedNode struct {
    key int
    value int
    prev *DLinkedNode
    next *DLinkedNode
} 

func initDLinkedNode(key, value int) *DLinkedNode {
    return &DLinkedNode{
        key: key,
        value: value,
    }
}

func Constructor(capacity int) LRUCache {
    l := LRUCache{
        capacity:capacity,
        cache map[int]*DLinkedNode{}
        head: initDLinkedNode(0, 0),
        tail: initDLinkedNode(0, 0),
    }

    l.head.next = l.tail
    l.tail.prev = l.head

    return l
}

func (this *LRUCache) Get(key int) int {
    if _, ok := this.cache[key]; !ok {
        return -1
    }
    node := this.cache[key]
    this.moveToHead(node)
    return node.value
}


func (this *LRUCache) Put(key int, value int)  {
    if _, ok := this.cache[key]; !ok {
        node := initDLinkedNode(key, value)
        this.cache[key] = node
        this.addToHead(node)
        this.size++
        if this.size > this.capacity {
            removed := this.removeTail()
            delete(this.cache, removed.key)
            this.size--
        }
    } else {
        node := this.cache[key]
        node.value = value
        this.moveToHead(node)
    }
}

func (this *LRUCache) addToHead(node *DLinkedNode) {
    node.prev = this.head
    node.next = this.head.next
    this.head.next.prev = node
    this.head.next = node
}

func (this *LRUCache) removeNode(node *DLinkedNode) {
    node.prev.next = node.next
    node.next.prev = node.prev
}

func (this *LRUCache) moveToHead(node *DLinkedNode) {
    this.removeNode(node)
    this.addToHead(node)
}

func (this *LRUCache) removeTail() *DLinkedNode {
    node := this.tail.prev
    this.removeNode(node)
    return node
}

```
