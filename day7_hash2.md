# 10.31 哈希表2

#### 454.

四数之和，将四个分成两组就是两数之和

```python

    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        hashmap = dict()
        for n1 in nums1:
            for n2 in nums2:
                if n1 + n2 in hashmap:
                    hashmap[n1 + n2] += 1
                else:
                    hashmap[n1 + n2] = 1
        
        # 如果 -(n1+n2) 存在于nums3和nums4, 存入结果
        count = 0 
        for n3 in nums3:
            for n4 in nums4:
                key = -(n3 + n4)
                if key in hashmap:
                    count += hashmap[key]
                    #有可能有两个加和相等的情况，（2+6/3+5之类的 
                    #所以可以加hashmap[key]
        
        return count
```
---
#### 383.

赎金信主要是最后一行代码，判断T/F

```python

    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        ransom_c = [0] * 26
        magazine_c = [0] * 26
        for i in magazine:
            magazine_c[ord(i) - ord("a")] += 1
        for i in ransomNote:
            ransom_c[ord(i) - ord("a")] += 1
        return all(ransom_c[i] <= magazine_c[i] for i in range(26))
    
    #利用counter
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        return not Counter(ransomNote) - Counter(magazine)
```

#### 15. 三数之和

这道题最复杂的是去重，所以用双指针来做比较好，定义了i，left，right三个指针，

记得要先sort数组，这样重复的就是连续的，比较好甄别去重。

右一定大于左。

```python

    def threeSum(self, nums: List[int]) -> List[List[int]]:
        result = []
        nums.sort()
        for i in range(len(nums)):
            #如果第一个元素已经大于0，不需要检查
            if nums[i] > 0:
                return result
            
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            #跳过相同元素

            left = i + 1
            right = len(nums) - 1

            while right > left:
                sum_ = nums[i] + nums[left] + nums[right]

                if sum_ < 0:
                    left += 1
                elif sum_ >0:
                    right -= 1
                else:
                    result.append([nums[i], nums[left], nums[right]])

                    while right > left and nums[right] == nums[right - 1]:
                        right -= 1
                    while right > left and nums[left] == nums[left + 1]:
                        left += 1
                
                    right -= 1
                    left += 1
        return result
```

#### 18. 四数之和

注意去重！尤其是去重的位置，里面的去重是在比较 s = target 之后再进行的。
外面剪枝操作想不明白可以不写

```python

    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        n = len(nums)
        result = [] 
        for i in range(n):
            //这里是剪枝操作
            if nums[i] > target and nums[i] > 0 and target > 0 :
                break
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            for j in range(i+1, n):
                if nums[i] + nums[j] > target and target > 0:
                    break
                if j > i+1 and nums[j] == nums[j - 1]:
                    continue
                left, right = j+1, n-1
                while left < right:
                    s = nums[i] + nums[j] + nums[left] + nums[right]
                    if s == target:
                        result.append([nums[i], nums[j], nums[left], nums[right]])
                        while left < right and nums[left] == nums[left+1]:
                            left += 1
                        while left < right and nums[right] == nums[right - 1]:
                            right -= 1
                        
                        left += 1
                        right -= 1
                    elif s < target:
                        left += 1
                    else:
                        right -= 1
        return result

```
