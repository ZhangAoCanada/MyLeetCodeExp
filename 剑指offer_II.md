# 一些剑指offer题解中较好的方法

## BitMask 存字母

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

还需要注意利用2D几何特征做的`matrix`前缀和，例如：[二维子矩阵的和](https://leetcode-cn.com/problems/O4NDxx/)和[向下的路径节点之和](https://leetcode-cn.com/problems/6eUYwP/)。

## 并查集

如果题目给出的数据类型是`图`，基本就是用这个方法没得跑了。例题：[最长连续序列](https://leetcode-cn.com/problems/WhsWhI/submissions/0)。

关于并查集的具体解释，可以参考[知乎](https://zhuanlan.zhihu.com/p/93647900/)。

方法：
```python
# 先建立一个图，让所有节点都指向自己
mp = {}
for n in nums:
    mp[n] = n
# 找到 n 的根结点
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

## 用小根堆/大根堆排序

排序是个比较常见的问题，经典算法像`mergeSort`，`quickSort`等等都得有一定的认知。

除了上述方法，小根堆/大根堆也经常会拿出来考，比如说[数组中第k大的数字](https://leetcode-cn.com/problems/xx4gT2/)。

## dfs 和 bfs

可以看出这两个出现频率可以说是很高了。

**注意**：需要注意的是，有时候会靠一些 dfs/bfs 的变种，比如说题目[开锁密码](https://leetcode-cn.com/problems/zlDJc7/)需要`双向 dfs`去解答。

## 拓扑排序

此方法是针对`有向无环图`的排序方法。对于`无向图`和`有环的有向图`，这个方法无法排序，所以此方法可以去验证数据结构是否为`有向无环图`。例题：[课程顺序](https://leetcode-cn.com/problems/QA2IGt/)。

## 双指针

这类算法经常会出现在`数组`或者`字符串`的问题中。例题如[数组中和为 0 的三个数](https://leetcode-cn.com/problems/1fGaJU/)和[最多删除一个字符得到回文](https://leetcode-cn.com/problems/RQku0D/)都是很好的例子。

## 关于字符串回文

一般情况下:
- 如果去判断一个字符串是否回文，可以使用`双指针`；
- 如果去从一个字符串中找出回文子字符串，可以从中间往两边扩散的方式去寻找。 

## 滑动窗口

又是一个很常见的算法，一般当题目中出现字眼如`连续子序列`的时候，就会考滑动窗口。
例题：[和大于等于 target 的最短子数组](https://leetcode-cn.com/problems/2VG8Kg/)。

## 二分

二分的本质很简单，就是一个`O(logn)`的搜索算法，其前提是数组是有序的。

现在的题目往往会出二分的变种，比如说[排序数组中只出现一次的数字](https://leetcode-cn.com/problems/skFtm2/)。

## 树

这类题目简单的一般都用`dfs`和`bfs`做；难的就真的随缘了。比如说`前序遍历`，`后序遍历`，`层次遍历`加上`广度优先搜索`，`深度优先搜索`混合着考等等。例题：[二叉搜索树中的中序后继](https://leetcode-cn.com/problems/P5rCT8/)。 

其中`二叉搜索树`比较喜欢考。有的题就喜欢把上面的全综合起来考，比如说[二叉搜索树中的中序后继题解](https://leetcode-cn.com/problems/P5rCT8/solution/tong-guan-jian-2-dfs-by-muluo-2-id3e/)

## 前缀树，又称字典书，活着`Trie`

这个可以用来检查两个字符串是否相同，活着是否一个是另一个的前缀，例题：[实现前缀树](https://leetcode-cn.com/problems/QC3q1f/)。

这个算法的应用也很广，具体使用方式也很花样。

## 堆

问考`大根堆`和`小根堆`哪家强，那得看题目：[和最小的 k 个数对](https://leetcode-cn.com/problems/qn8gGX/)。
此题厉害在于用`大根堆`和`小根堆`都能解，其中`小根堆`利用了题目中数组的特性而可以更快解答。

## “简单”的 `DP`

`DP`当之无愧成了现在最难想的算法，个个题目如同脑经急转弯一样。

那些把我做飞的题目：
- [前 n 个数字二进制中 1 的个数](https://leetcode-cn.com/problems/w3tCBm/})
- [回文子字符串的个数](https://leetcode-cn.com/problems/a7VOhD/)
- []()
- []()