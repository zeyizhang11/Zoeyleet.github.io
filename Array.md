<<<<<<< HEAD
# 代码随想Carl --- 1. 数组Array

数组是存放在连续内存空间上的相同类型数据的集合。
数组可以方便的通过下标索引的方式获取到下标下对应的数据。

1. 数组下标都是从0开始的
2. 数组内存空间的地址是*连续的*/所以我们在删除或者增添元素的时候，就难免要移动其他元素的地址。
3. 数组的元素是*不能删的，只能覆盖*。

---

	```python
    #704
    # 区间的定义就是不变量。要在二分查找的过程中，保持不变量，
    # 就是在while寻找中每一次边界的处理都要坚持根据区间的定义来操作，这就是循环不变量规则

    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) #[) 
        #Another way is [] notice: mid - 1

        while left < right: 
            mid = left + (right - left) // 2
            if nums[mid] > target:
                right = mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                return mid
        
        return -1
	
	```
---

    ```python
    #27
    def removeElement(self, nums: List[int], val: int) -> int:
    #two index
        slow = 0
        fast = 0
        size = len(nums)
        while fast < size:
            if nums[fast] != val:
                #slow collect the different value
                nums[slow] = nums[fast]
                slow += 1
                # when there is a different value
                #slow add 1
            fast += 1
        return slow
	
	```


=======
# 代码随想Carl --- 1. 数组Array

数组是存放在连续内存空间上的相同类型数据的集合。
数组可以方便的通过下标索引的方式获取到下标下对应的数据。

1. 数组下标都是从0开始的
2. 数组内存空间的地址是*连续的*/所以我们在删除或者增添元素的时候，就难免要移动其他元素的地址。
3. 数组的元素是*不能删的，只能覆盖*。

---

	```python
    #704
    # 区间的定义就是不变量。要在二分查找的过程中，保持不变量，
    # 就是在while寻找中每一次边界的处理都要坚持根据区间的定义来操作，这就是循环不变量规则

    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) #[) 
        #Another way is [] notice: mid - 1

        while left < right: 
            mid = left + (right - left) // 2
            if nums[mid] > target:
                right = mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                return mid
        
        return -1
	
	```
---

    ```python
    #27
    def removeElement(self, nums: List[int], val: int) -> int:
    #two index
        slow = 0
        fast = 0
        size = len(nums)
        while fast < size:
            if nums[fast] != val:
                #slow collect the different value
                nums[slow] = nums[fast]
                slow += 1
                # when there is a different value
                #slow add 1
            fast += 1
        return slow
	
	```


>>>>>>> c61bbc78f0c42a5217de16057866ce45f6425743
