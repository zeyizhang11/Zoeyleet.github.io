# 11.1 字符串

#### 344. 反转字符串

双指针 用 while 比 for 更快

```python

    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left = 0
        right = len(s) - 1
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
```
---
#### 541.反转字符串2

注意这个pythonic的应用！
取从后向前（相反）的元素

```python

  def reverseStr(self, s: str, k: int) -> str:
        n = len(s)
        i = 0
        while i < n:
            j = i + k 
            s = s[:i] + s[i : j][::-1] + s[j:] 
            #这个小trick，取从后向前（相反）的元素
            i = i + 2*k
        return s 

```

#### 翻转字符串里的单词

['Line1-abcdef', 'Line2-abc', 'Line4-abcd'] 分割结果类似这样

```python
    def reverseWords(self, s: str) -> str:
        words = s.split()

        left = 0
        right = len(words) - 1

        while left < right:
            words[left], words[right] = words[right], words[left]
            left += 1
            right -= 1
        
        return " ".join(words)
```
