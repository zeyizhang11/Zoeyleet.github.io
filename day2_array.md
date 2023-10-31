# 代码随想Carl --- 2. 数组Array 10.26

## 977.有序数组的平方（双指针）

注意有序数组的平方，首尾两端存在最大值。

所以可以使用双指针，（i，j），再单独来个k指针在新数组从右到左（从大到小）的保存。


```python

    def sortedSquares(self, nums: List[int]) -> List[int]:
        i = 0
        j = len(nums) - 1
        result = [0] * len(nums)
        k = len(nums) - 1

        while k >= 0:
            if nums[i]**2 < nums[j]**2:
                result[k] = nums[j]**2
                j -= 1
            else:
                result[k] = nums[i]**2
                i += 1

            k -= 1
        
        return result
	
```
---
## 209.长度最小的子数组（滑动窗口）

滑动窗口，就是不断的调节子序列的起始位置和终止位置，从而得出我们要想的结果。

只用一个for循环，那么这个循环的索引，一定是表示 滑动窗口的终止位置。（两个for就是暴力解法了）

窗口就是 满足其和 ≥ s 的长度最小的 连续 子数组。

窗口的起始位置如何移动：如果当前窗口的值大于s了，窗口就要向前移动了（也就是该缩小了）。

窗口的结束位置如何移动：窗口的结束位置就是遍历数组的指针，也就是for循环里的索引。

滑动窗口的精妙之处在于根据当前子序列和大小的情况，不断调节子序列的起始位置。从而将O(n^2)暴力解法降为O(n)。

```python

    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l = len(nums)
        j = 0 #end
        i = 0 #start
        cur_sum = 0
        min_len = float('inf') #max value

        while j < l: #j at the first
            cur_sum += nums[j]

            while cur_sum >= target:
                min_len = min(min_len, j-i+1)
                cur_sum -= nums[i]
                i += 1
        
            j += 1
        return min_len if min_len != float('inf') else 0
	
```

---
## 59.螺旋矩阵（坚持左闭右开）

就是个仔细！！！不行就画图！

```python

    def generateMatrix(self, n: int) -> List[List[int]]:
        nums = [[0] * n for _ in range(n) ] # n*n matrix
        startx, starty = 0, 0 #start
        loop, mid = n // 2, n // 2 # 迭代次数、n为奇数时，矩阵的中心点
        count = 1

        for offset in range(1, loop+1): # 每循环一圈，修改的步数 [1,2)
            for i in range(starty, n-offset): # 从0开始，n-offset = 3-1 =2 从左到右两步 [0,2)
                nums[startx][i] = count # 第0排，1，2
                count += 1
            for i in range(startx, n-offset): # 从上到下 [0,2):0,1
                nums[i][n - offset] = count #[0][2]  [1][2]
                count += 1
            
            for i in range(n-offset, starty, -1): # 从右到左 [2,0) 2,1
                nums[n-offset][i] = count #从右到左 [2][2],[2][1]
                count += 1
            
            for i in range(n-offset, startx, -1): # 从下到上 [2,0) 2,1
                nums[i][starty] = count
                count += 1
            
            startx += 1
            starty += 1 # 对角线向下第二层
        
        if n%2 != 0 : # n is odd, fill the central point
            nums[mid][mid] = count
        return nums
```