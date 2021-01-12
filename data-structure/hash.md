# 散列表

### 结构

* HashMap  //未排序，时间复杂度O(1)
* HashSet
* TreeMap  //已经排序，时间复杂度O(logn)
* TreeSet

理想散列表（哈希表）是一个包含关键字的具有固定大小的数组，它能够以常数时间执行插入，删除和查找操作。
每个关键字被映射到0到数组大小N-1范围，并且放到合适的位置，这个映射规则就叫散列函数
理想情况下，两个不同的关键字映射到不同的单元，然而由于数组单元有限，关键字范围可能远超数组单元，因此就会出现两个关键字散列到同一个值得时候，这就是散列冲突

### 冲突解决

- 拉链法，分离链接法的做法是将同一个值的关键字保存在同一个表中。
- 开放定址法 - 如果冲突发生，就选择另外一个可用的位置。
  - 线性探测法
  - 平方探测法
  - 双散列

### [判断是否为异位词](https://leetcode-cn.com/problems/valid-anagram/description/)

方法1，两个字符串排序后，比较是否相同

```golang
func isAnagram(s, t string) bool {
    s1, s2 := []byte(s), []byte(t)
    sort.Slice(s1, func(i, j int) bool { return s1[i] < s1[j] })
    sort.Slice(s2, func(i, j int) bool { return s2[i] < s2[j] })
    return string(s1) == string(s2)
}
```

方法2，使用Map计数

```golang
func isAnagram(s string, t string) bool {
    var sa, ta [26]int

    for _, ch := range s {
        sa[ch - 'a']++
    }

    for _, ch := range t {
        ta[ch - 'a']++
    }

    return sa == ta
}
```

### [两数之和](https://leetcode-cn.com/problems/two-sum/description/)

```golang
func twoSum(nums []int, target int) []int {
    numMap := make(map[int]int, 0)
    for k, v := range nums {
        if p, ok := numMap[target - v]; ok {
            return []int{k, p}
        }

        numMap[v] = k
    }

    return nil
}
```

### [三数之和](https://leetcode-cn.com/problems/3sum/description/)

```golang
func threeSum(nums []int) [][]int {
    var results [][]int
    sort.Ints(nums)
    for k, v := range nums {
        if k > 0 && nums[k] == nums[k-1] {
            continue
        }

        left, right := k+1, len(nums)-1
        for left < right {
            value := v + nums[left] + nums[right]
            if value == 0 {
                results = append(results, []int{v, nums[left], nums[right]})
                left++
                right--

                for left < right && nums[left] == nums[left-1] {
                    left++
                }
                for left < right && nums[right] == nums[right+1] {
                    right--
                }
            } else if value < 0 {
                left++
            } else if value > 0 {
                right--
            }
        }
    }

    return results
}
```

### [四数之和](https://leetcode-cn.com/problems/4sum/)

### [字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/description/)
