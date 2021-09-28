# 一些剑指offer题解中较好的方法

## 找不含相同字符的两个字符串（利用32位二进制储存26个字母）(算属于Hash Map类)

此方法即利用一个32位的整数去储存每一个字符串中出现的字母，然后比较两个整数的二进制表示是否相同或不同即可。例题：[单词长度的最大乘积](https://leetcode-cn.com/problems/aseY1I/submissions/)。

方法：
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

## 前缀和

此方法可以应用到树结构或者数组中，应用比较广泛。例题：[路径总和III](https://leetcode-cn.com/problems/path-sum-iii/)

## 并查集

如果题目给出的数据类型是`图`，基本就是用这个方法没得跑了。例题：[最长连续序列](https://leetcode-cn.com/problems/WhsWhI/submissions/0)。

关于并查集的具体解释，可以参考[知乎](https://zhuanlan.zhihu.com/p/93647900/)。

方法：
```python
# 先建立一个图，让所有节点都指向自己
mp = {}
for n in nums:
    mp[n] = n
# 找到 n 的根结点
def findFather(n):
    if mp[n] == n: return n
    return findFather(mp[n])
# 如果 i, j 有联系，讲 j 的根结点指向 i
def merge(i, j):
    father_i = findFather(i)
    father_j = findFather(j)
    if father_i != father_j:
        mp[father_j] = father_i 
```

## 栈

纯考数据结构类型的题不多，一般会寄托着一起考某些经典算法，比如出现于[后缀表达式](https://leetcode-cn.com/problems/8Zf90G/)里面的[逆波兰式](https://baike.baidu.com/item/%E9%80%86%E6%B3%A2%E5%85%B0%E5%BC%8F/128437)就是使用栈的方法。

此外，另一种类型的栈，`单调栈`出现的几率可能比普通的`栈`要更大。

## 链表

针对此数据类型，一般考的是`快慢指针找中点`，`快慢指针找重合点`，`reverseLinklist`等。比如，例题[重排链表](https://leetcode-cn.com/problems/LGjMqU/)就包含了其中的两个方法。

链表的考点多侧重于逻辑，比如说链表的差值，倒序等等。

## 排序