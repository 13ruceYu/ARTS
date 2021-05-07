# week_001

## Algorithm

### 什么是数据结构和算法

从广义上讲，数据结构就是一组数据的存储结构，算法就是操作数据的一种方法。

数据结构是为算法服务的，算法要作用在特定的数据结构之上，因此，我们无法孤立数据结构来讲算法，也无法孤立算法来讲数据结构。

数据结构是静态的，只是组织数据的一种方式。如果不在它的基础上操作、构建算法，孤立存在的数据结构是没有用的。

### 复杂度分析

复杂度分析是数据结构和算法中最重要的概念，是数据结构和算法学习的精髓。

数据结构和算法解决的是如何更省、更快的存储和处理数据，这就需要考量**效率**和资源消耗，也就是复杂度分析。它帮我们量化了数据结构和算法解决问题的效率和资源的消耗。

在搞定复杂度分析后，我们就可以开始数据结构和算法的正文内容了。

其中包括 10 个数据结构：

1. 数组
2. 链表
3. 栈
4. 队列
5. 二叉树
6. 堆
7. 跳表
8. 图
9. Tire
10. 树

10 个算法：

1. 递归
2. 排序
3. 二分查找
4. 搜索
5. 哈希算法
6. 贪心算法
7. 分治算法
8. 回溯算法
9. 动态规划
10. 字符串匹配算法

### 大 O 复杂度表示法

算法代码的执行时间和每行代码的执行次数成正比，用 T(n)=O(f(n)) 表示，T(n) 表示代码执行时间，n 表示数据规模的大小，f(n) 表示每行代码执行次数的总和。O 表示代码的执行时间 T(n) 与 f(n) 表达式成正比。

以时间复杂度为例，由于时间复杂度描述的是算法执行时间与数据规模增长的变化趋势，f(n) 公式中的低阶，常量，系数三部分并不左右增长趋势，可忽略。

### 复杂度分析法则

1. 单段代码看高频：比如循环。
2. 多段代码取最大值：比如一段代码中既有单循环，又有多重循环，那么取多重循环的复杂度。
3. 嵌套代码求乘积：比如递归，多重循环等。
4. 多个规模求加法：比如两个参数控制两个循环的次数，那么就取二者复杂度相加。

### 复杂度量级

常见复杂度量级可粗略分为两类：

* 多项式量级（Deterministic Polynomial）
* 非多项式量级（Non-Deterministic Polynomial）

非多项式量级只有两个：O(2^n)（指数阶） 和 O(n!)（阶乘阶），都是非常低效的算法，可以不用展开了解。

多项式复杂度量级：

1. O(1)：常数阶
2. O(logn)：对数阶
3. O(n)：线性阶
4. O(nlogn)：线性对数阶
5. O(n^2)：平方阶
6. O(n^3)：立方阶

### 算法题

[二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

```js
/* 
剑指 Offer 04. 二维数组中的查找 
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

示例:

现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。

限制：

0 <= n <= 1000

0 <= m <= 1000
*/
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var findNumberIn2DArray = function(matrix, target) {
  if (!matrix || matrix.length === 0) {
    return false;
  }

  let row = matrix.length,
      col = matrix[0].length,
      x = col - 1,
      y = 0;
  
  while (x >= 0 && y < row) {
    if (matrix[y][x] === target) {
        return true;
    }
    matrix[y][x] > target ? x-- : y++;
  }
  return false;
};
```

当以 matrix 的左下角或者右上角开始查找时，这个问题就变成了 Binary Search Tree。

复杂度分析：

* 时间复杂度：O(m+n)；
* 空间复杂度：O(1)。

## Review

[Starting with an idea and building a community](https://github.com/readme/evan-you)

In this article, Evan You(creator of Vue) shared the following points:

* the birth of Vue
* why he decided to be a full-time open-source maintainer
* suggestions for open source enthusiast

## Tip

[Vue 页面初始化数据请求应该放在 created or mounted](https://cq036pgwqz.feishu.cn/docs/doccnSXl1UzyTl4EuvkuVPnHG6b)

## Share

[OKR的优势：为什么要用OKR来取代KPI做团队规划？](https://time.geekbang.org/column/article/334826)
