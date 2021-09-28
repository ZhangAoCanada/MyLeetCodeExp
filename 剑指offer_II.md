# 一些剑指offer题解中较好的方法

## Hash Map

### 找不含相同字符的两个字符串（利用32位二进制储存26个字母）

此方法即利用一个32位的整数去储存每一个字符串中出现的字母，然后比较两个整数的二进制表示是否相同或不同即可。例题：[单词长度的最大乘积](https://leetcode-cn.com/problems/aseY1I/submissions/)。方法：
```python
# 利用32位整数去储存每一个字符串中出现的字母
for i in range(len(words)):
    for c in words[i]:
        mp[i] |= (1 << (ord(c) - ord("a")))
# 比较两个整数的二进制表示是否相同或不同
for i in range(len(words)):
    for j in range(i + 1, len(words)):
        if mp[i] & mp[j] == 0:
            # i, j 为两个不包含一样字符的字符串
```