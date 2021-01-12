# 优先队列

- 普通的队列是一种先进先出的数据结构，元素在队列尾追加，而从队列头删除。
- 在优先队列中，元素被赋予优先级。当访问元素时，具有最高优先级的元素最先删除。
- 优先队列具有最高级先出 （first in, largest out）的行为特征。
- 通常采用堆数据结构来实现。

## [滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

### 方法1.使用大顶堆

### 方法2

```golang
func maxSlidingWindow(nums []int, k int) []int {
    if len(nums) == 0 {
        return []int{}
    }

    var windows, res []int

    for i, x := range nums {
        if i >= k && windows[0] <= i - k {
            windows = windows[1:len(windows)]
        }

        //如果window最后一个元素小于新加入的元素，删除最后一个元素
        for len(windows) > 0 &&  nums[windows[len(windows)-1]] <= x {
            windows = windows[:len(windows)-1]
        }

        windows = append(windows, i)
        if i >= k -1 {
            res = append(res, nums[windows[0]])
        }
    }

    return res
}
```

## [数据流中的第 K 大元素](https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/)

- 维护一个长度为k的小顶堆
- 循环数组，往小顶堆插入元素
- 如果小于堆顶元素，直接舍弃。如果大于堆顶元素，插入元素，舍弃堆顶元素
- 返回堆顶元素

