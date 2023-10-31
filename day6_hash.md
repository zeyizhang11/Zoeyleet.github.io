# 10.30 哈希表

哈希表是根据关键码的值而直接进行访问的数据结构。其实直白来讲其实数组就是一张哈希表。

哈希表中关键码就是数组的索引下标，然后通过下标直接访问数组中的元素。

一般哈希表都是用来快速判断一个元素是否出现集合里。例如要查询一个名字是否在这所学校里。要枚举的话时间复杂度是O(n)，但如果使用哈希表的话， 只需要O(1)就可以做到。


#### 242.

这道题就是先加后减，利用只有26个字母的数组。


```python

    def isAnagram(self, s: str, t: str) -> bool:
        record = [0] * 26
        for i in s:
            record[ord(i)- ord("a")] += 1
        for i in t:
            record[ord(i)- ord("a")] -= 1
        for i in range(26):
            if record[i] != 0:
                return False
        return True
	
```
---

#### 349 

这道题两个数组，所以可以考虑两个数组（而且数据量少），交集就是两个数组都不为零的部分。

```python

    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        count1 = [0]*1001
        count2 = [0]*1001
        result = []
        for i in range(len(nums1)):
            count1[nums1[i]] += 1
        for j in range(len(nums2)):
            count2[nums2[j]]+=1
        for k in range(1001):
            if count1[k]*count2[k]>0:
                result.append(k)
        return result
	
```

#### 202

快乐数要抓住无限循环的和
无限循环，那么也就是说求和的过程中，sum会重复出现，这对解题很重要！

当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法了。

所以这道题目**使用哈希法，来判断这个sum是否重复出现，如果重复了就是return false， 否则一直找到sum为1为止**

```python

    def isHappy(self, n: int) -> bool:
        record = []
        while n not in record:
            record.append(n)
            new_num = 0
            n_str = str(n)
            for i in n_str:
                new_num += int(i)**2
            if new_num == 1: 
                return True
            else: 
                n = new_num #不重复出现就加进去
        return False
	
```
#### 1

enumerate()返还值和index， 加到字典里，来比对 重点是**两数之和**

```python

    def twoSum(self, nums: List[int], target: int) -> List[int]:
        records = dict()

        for index, value in enumerate(nums):
            if target -value in records:
                return [records[target- value], index]
            records[value] = index
        return []
	
```
