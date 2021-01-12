# 分治算法

根据字面意思解释是“分而治之”，就是把一个复杂的问题分成两个或更多的相同或相似的子问题，再把子问题分成更小的子问题，直到最后子问题可以简单的直接求解，原问题的解即子问题的解的合并。

## 汉诺塔

古代有一个梵塔，塔内有三个座A、B、C，A座上有64个盘子，盘子大小不等，大的在下，小的在上。有一个和尚想把这个盘子从A座移到B座，但每次只能允许移动一个盘子，并且在移动过程中，3个座上的盘子始终保持大盘在下，小盘在上。

- 如果只有1个盘子，则不需要利用B塔，直接将盘子从A移动到C。
- 如果有2个盘子，可以先将盘子2上的盘子1移动到B，将盘子2移动到C，将盘子1移动到 C 。这说明了：可以借助B将2个盘子从A移动到C。
- 如果有3个盘子，那么根据2个盘子的结论，可以借助 C 将盘子 3 上的两个盘子从 A 移动到 B ；将盘子 3 从 A 移动到 C ，A 变成空座；借助 A 座，将 B 上的两个盘子移动到 C 。
- 以此类推，上述的思路可以一直扩展到 n 个盘子的情况，将将较小的 n-1个盘子看做一个整体，也就是我们要求的子问题，以借助 B 塔为例，可以借助空塔 B 将盘子A上面的 n-1 个盘子从 A 移动到 B ；将A 最大的盘子移动到 C ， A 变成空塔；借助空塔 A ，将 B 塔上的 n-2 个盘子移动到 A，将 C 最大的盘子移动到 C， B 变成空塔。。。

## [Pow(x, n)](https://leetcode-cn.com/problems/powx-n/description/)

```golang

func myPow(x float64, n int) float64 {
    if n == 0 {
        return 1
    } else if n < 0 {
        return 1 / myPow(x, -n)
    } else if n % 2 == 1 {
        return x * myPow(x, n-1)
    } else {
        return myPow(x*x, n/2)
    }
}
```

## [多数元素](https://leetcode-cn.com/problems/majority-element/description/)

## [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/description/)

## [有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/#/description)

## [找到字符串中所有字母异位词](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/#/description)

## [](https://leetcode-cn.com/problems/anagrams/#/description)
