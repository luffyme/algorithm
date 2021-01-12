# 动态规划

## 步骤

- 递归+记忆化 —> 递推
- 状态的定义：opt[n], dp[n], fib[n]
- 状态转移⽅程：opt[n] = best_of(opt[n-1], opt[n-2], …)
- 记录最优子结构

## [爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/description/)

爬第n阶楼梯的方法数量，等于 2 部分之和

- 爬上 n-1 阶楼梯的方法数量。因为再爬1阶就能到第n阶
- 爬上 n-2 阶楼梯的方法数量，因为再爬2阶就能到第n阶

所以我们得到公式 dp[n] = dp[n-1] + dp[n-2]dp[n]=dp[n−1]+dp[n−2]

同时需要初始化 dp[0]=1和dp[1]=2

时间复杂度：O(n)O(n)

```golang

//动态规划解法
func climbStairs(n int) int {
    p, q, r := 0, 0, 1
    for i := 1; i <= n; i++ {
        p = q
        q = r
        r = p + q
    }
    return r
}

//其他解法
func climbStairs(n int) int {
    mem := []int{0, 1, 2}
    for i := 3; i <= n; i++ {
        mem[i] = mem[i-1] + mem[i-2]
    }
    
    return mem[n]
} 
```

## [三角形最小路径和](https://leetcode-cn.com/problems/triangle/description/)

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。相邻的结点 在这里指的是 下标 与 上一层结点下标 相同或者等于 上一层结点下标 + 1 的两个结点。

例如，给定三角形：

```text
[
        [2],
    [3,4],
    [6,5,7],
    [4,1,8,3]
]
```

自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。

状态定义：dp[i][j]dp[i][j] 表示从点 (i, j)(i,j) 到底边的最小路径和。

状态转移：dp[i][j] = min(dp[i + 1][j], dp[i + 1][j + 1]) + triangle[i][j]dp[i][j]=min(dp[i+1][j],dp[i+1][j+1])+triangle[i][j]

```golnag
func minimumTotal(triangle [][]int) int {
    // 计算行数
    n := len(triangle)
    dp := make([][]int, n)
    
    // 初始化
    for i := 0; i < n; i++ {
        dp[i] = make([]int, n)
    }
    
    for i := n - 1; i >= 0; i-- {
        for j = 0; j <= i; j++ {
            dp[i][j] = min(dp[i+][j], dp[i+][j+1]) + triangle[i][j]
        }
    }
    
    return dp[0][0]
}

func min(x, y int) int {
    if x < y {
        return x
    }
    return y
}
```

但是在实际递推中我们发现，计算 `dp[i][j]dp[i][j]` 时，只用到了下一行的 `dp[i + 1][j]dp[i+1][j]` 和 `dp[i + 1][j + 1]dp[i+1][j+1]`。因此 dpdp 数组不需要定义 NN 行，只要定义 11 行就阔以啦。

```golnag
func minimumTotal(triangle [][]int) int {
    // 计算行数
    n := len(triangle)
    dp := triangle[n-1]
    
    for i := n - 1; i >= 0; i-- {
        for j = 0; j <= i; j++ {
            dp[j] = min(dp[i+][j], dp[i+][j+1]) + triangle[i][j]
        }
    }
    
    return dp[0]
}


## 最大子序和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

输入: [-2,1,-3,4,-1,2,1,-5,4],

输出: 6

解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。如果我们确定一个子数组的截止元素在 i 这个位置，这个时候我们需要思考的问题是 “以 i 结尾的所有子数组中，和最大的是多少？”

然后我们去试着拆解，这里其实只有两种情况：
- i 这个位置的元素自成一个子数组;
- i 位置的元素的值 + 以 i - 1 结尾的所有子数组中的子数组和最大的值

通过上面的分析，其实状态已经有了，dp[i] 就是 “以 i 结尾的所有子数组的最大值”，递推方程：

```text
dp[i] = Math.max(dp[i - 1] + array[i], array[i])
dp[i] = Math.max(dp[i - 1], 0) + array[i]
```

函数：

```golnag
public int maxSubArray(int[] nums) {
    if (nums == null || nums.length == 0) {
        return 0;
    }

    int n = nums.length;
    int[] dp = new int[n];
    dp[0] = nums[0];
    int result = dp[0];

    for (int i = 1; i < n; ++i) {
        dp[i] = Math.max(dp[i - 1], 0) + nums[i];
        result = Math.max(result, dp[i]);
    }

    return result;
}
```

## [](https://leetcode-cn.com/problems/triangle/description/)

## [](https://leetcode-cn.com/problems/maximum-product-subarray/description/)

## [](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/#/description)

## [](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

## [](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

## [](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)

## [](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

## [](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

## [](https://leetcode-cn.com/problems/longest-increasing-subsequence)

## [](https://leetcode-cn.com/problems/coin-change/)

## [](https://leetcode-cn.com/problems/edit-distance/)
