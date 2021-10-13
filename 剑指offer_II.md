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

另外，还有些堆的题目会需要多想一会，比如，问考`大根堆`和`小根堆`哪家强，那得看题目：[和最小的 k 个数对](https://leetcode-cn.com/problems/qn8gGX/)。
此题厉害在于用`大根堆`和`小根堆`都能解，其中`小根堆`利用了题目中数组的特性而可以更快解答。

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

## 双指针+二分

这类题目喜欢把两个概念参杂起来考，很考验自己对各种方法的理解。例如：[排序矩阵查找](https://leetcode-cn.com/problems/sorted-matrix-search-lcci/)

## 树

这类题目简单的一般都用`dfs`和`bfs`做；难的就真的随缘了。比如说`前序遍历`，`序遍历`，`后序层历`加上`广度优先搜索`，`深度优先搜索`混合着考等等。例题：[二叉搜索树中的中序后继](https://leetcode-cn.com/problems/P5rCT8/)。 

其中`二叉搜索树`比较喜欢考。有的题就喜欢把上面的全综合起来考，比如说[二叉搜索树中的中序后继题解](https://leetcode-cn.com/problems/P5rCT8/solution/tong-guan-jian-2-dfs-by-muluo-2-id3e/)

## 前缀树，又称字典书，或者`Trie`

这个可以用来检查两个字符串是否相同，活着是否一个是另一个的前缀，例题：[实现前缀树](https://leetcode-cn.com/problems/QC3q1f/)。

这个算法的应用也很广，具体使用方式也很花样。

## “简单”的 `DP`

`DP`当之无愧成了现在最难想的算法，个个题目如同脑经急转弯一样。

那些把我做飞的题目：
- [前 n 个数字二进制中 1 的个数](https://leetcode-cn.com/problems/w3tCBm/})：想不出来啊。
- [回文子字符串的个数](https://leetcode-cn.com/problems/a7VOhD/)：还是想不出来啊。
- [最长公共子序列](https://leetcode-cn.com/problems/qJnOS7/)：所以人老了，这么典型的`DP`没做出来。
- [字符串交织](https://leetcode-cn.com/problems/IY6buf/)：这个题又双叒叕没想出来，是不是真的老了。。。

## 区间`DP`

比较适用于需要从小区间慢慢往上积累到整体的`DP`算法，目前还是算比较难想的。典型例题：[布尔运算](https://leetcode-cn.com/problems/boolean-evaluation-lcci/)。

## 来吧，背包（`0-1背包` 和 `完全背包`）

详细的解释可以在[这里](https://leetcode-cn.com/problems/D0F0SV/solution/tong-guan-jian-2-shuang-bai-bei-bao-dp-b-f33v/)看到。

为了方便，我还是把这个搬过来吧。。。

### `0-1背包`，即数组中的元素选取0次或者1次

有一个容量为 `N` 的背包，要用这个背包装下物品的价值最大，这些物品有两个属性：体积 `w` 和价值 `v`。

定义一个二维数组 `dp` 存储最大价值，其中 `dp[i][j]` 表示前 `i` 件物品体积不超过 `j` 的情况下能达到的最大价值。设第 `i` 件物品体积为 `w`，价值为 `v`，根据第 `i` 件物品是否添加到背包中，可以分两种情况讨论：

1. 第 `i` 件物品没添加到背包，总体积不超过 `j` 的前 `i` 件物品的最大价值就是总体积不超过 `j` 的前 `i-1` 件物品的最大价值，`dp[i][j] = dp[i-1][j]`。
2. 第 `i` 件物品添加到背包中，`dp[i][j] = dp[i-1][j-w] + v`。

第 `i` 件物品可添加也可以不添加，取决于哪种情况下最大价值更大。因此，`0-1背包`的状态转移方程为：
```cpp
dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - w] + v);
```
### 空间优化

在程序实现时可以对 `0-1背包`做优化。观察状态转移方程可以知道，前 `i` 件物品的状态仅与前 `i-1` 件物品的状态有关，因此可以将 `dp` 定义为一维数组，其中 `dp[j]` 既可以表示 `dp[i-1][j]` 也可以表示 `dp[i][j]`。此时，
```cpp
dp[j] = max(dp[j], dp[j - w] + v);
```
因为 `dp[j-w]` 表示 `dp[i-1][j-w]`，因此不能先求 `dp[i][j-w]`，防止将 `dp[i-1][j-w]` 覆盖。也就是说要先计算 `dp[i][j]` 再计算 `dp[i][j-w]`，在程序实现时需要按倒序来循环求解。

### `0-1背包`循环顺序

*`0-1背包`中二维 `dp` 数组的两个 `for` 遍历的先后循序是可以颠倒*

`dp[i][j]` 表示:

- 前 `i` 件物品
- 体积不超过 `j`
- 能达到的最大价值，我们之前已经分析出来了状态转移方程，但是循环的顺序应该怎样呢？
```cpp
for (int i = 0; i < nums.size(); ++i)
    for (int j = 0; j <= 背包容量; ++j)
        dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - w] + v);
```
```cpp
for (int j = 0; j <= 背包容量; ++j)
    for (int i = 0; i < nums.size(); ++i)
        dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - w] + v);
```

先遍历 物品还是先遍历背包重量呢？

其实都可以！！但是先遍历物品更好理解。（因为需要的  `dp[i - 1][j]` , `dp[i - 1][j - w]`  都在左上方向）

我们还是画图来理解下，数字代表遍历到的顺序

#### 先遍历物品
```
 ————————————>背包容量
| 1 2 3 4 5 6
| 7 8 9 ....
|
|
v
物品
```

#### 先遍历背包重量
```
 ————————————>背包容量
| 1  6 
| 2  7
| 3  8
| 4  9
v 5  ...
物品
```

两种方式，左上的值都是更新过的因此都可

一维 `dp` 数组的两个 `for` 循环先后循序一定是先遍历物品，再遍历背包容量。
```cpp
for (int i = 0; i < nums.size(); ++i)
    for (int j = 背包容量; j >= w ; --j)    // 防止越界j >= w
        dp[j] = max(dp[j], dp[j - w] + v);
```

很简单如果先遍历物品，走到7的时候左上的信息还在
```
 ————————————>背包容量
| 6 5 4 3 2 1 
|   ... 9 8 7         
| 
| 
v 
物品
```

#### 如果先遍历背包容量（错误）

那么这个顺序，我们可以清楚分析到一点，从`1->5`一开始就错了，因为6的信息还没有，但是`2`应该由`1` 和 `6` 以及 `6`同行的信息（左上）得到。
```
 ————————————>背包容量
|        6   1 
|        7   2  
|        8   3
|        9   4 
|      ...   5
|
v 
```

### 完全背包，元素可重复使用

1. 与`0-1背包`的区别主要是空间优化的时候正序就行
2. 在完全背包中，不论空间是二维，还是优化为一维，两个for循环嵌套顺序同样无所谓！

因为 `dp[j]` 是根据 下标j之前所对应的 `dp[j]` 计算出来的（左上）。只要保证下标 `j` 之前的 `dp[j]` 都是经过计算的就可以了。

#### 先遍历物品
```
 ————————————>背包容量
| 1 2 3 4 5 6
| 7 8 9 ....
|
|
v
物品
```

#### 先遍历背包重量
```
 ————————————>背包容量
| 1  6 
| 2  7
| 3  8
| 4  9
v 5  ...
物品
```

### 关于背包的经典例题：

- [分割等和子集](https://leetcode-cn.com/problems/NUPfPr/)：`0-1背包`
- [排列的数目](https://leetcode-cn.com/problems/D0F0SV/)：`完全背包`，这一题涉及到排序的问题，所以在使用两个循环语句的时候应该先遍历背包容量，再遍历物品，这样能是的原数组中不同元素的顺序可变。
- [加减的目标值](https://leetcode-cn.com/problems/YaVDxD/)：明显还不熟练啊。。。
- [最少的硬币数目](https://leetcode-cn.com/problems/gaM7Ch/)：完全背包两个方向都是可以的啊。。。