# week_003

## Algorithm

### 数据结构-链表（Linked list）

课前问题：LRU（Least Recently Used） 缓存淘汰算法？

#### 什么是链表？

从**底层存储结构**上看，数组需要一块连续的内存空间来存储，而链表不需要，链表通过“指针”将一组零散的内存块串联起来使用。所以如果我们申请一个 100 MB 大小的数组，当内存中没有连续的、足够大的存储空间时，即便总剩余空间大于 100 MB，仍会申请失败，如果申请 100 MB 的链表就会不会有这个问题。

![linked list structrue](images/linked_list_01.jpeg)

#### 链表分类

1. 单链表
2. 双向链表
3. 循环列表

链表是通过指针将一组零散的内存块串联在一起。我们把内存块称为链表的**“结点”**。每个链表的结点处了存储数据之外，还需要记录下一个结点的地址。记录下个结点地址的指针称为**后继指针 next**。

![单链表](images/linked_list_02.jpeg)

第一个结点叫作头节点，最后一个结点叫作尾结点。头结点用来记录链表的基地址，帮助我们遍历整条链表。尾结点不指向下一个结点，而是指向空地址 null。

与数组一样，链表也支持数据的查找、插入和删除操作。

数组插入、删除操作时，为了保持内存数据的连续性，需要做大量的数据搬移，所以时间复杂度为 O(n)。

链表插入、删除操作时，不用了为了保持数据的连续性而搬移结点，所以插入和删除一个数据是非常快速的。只需要改变的相临结点的指针改变，所以对应的时间复杂度是 O(1)。

![linked_list_operations](images/linked_list_03.jpeg)

有利就有弊，链表想要随机访问第 k 个元素，就没有数组那么高效了。

循环链表是特殊的单链表，唯一的区别在于尾结点。单链表的尾结点指向 null，循环链表的尾结点指向首结点。

![ll](images/linked_list_04.jpeg)

与单链表相比，循环链表的优点是从链头到链尾比较方便。当要处理的数据具有环形结构的特点时就比较合适。比如著名的**约瑟夫问题**。

![ll](images/linked_list_05.jpeg)

双向链表，顾名思义，它支持两个方向，每个结点不止有一个后继指针 next 指向后面的结点，还有一个前驱指针 prev 指向前面的结点。所以双向链表需要额外的两个空间来存储后继结点和前驱结点的地址。虽然两个指针比较浪费存储空间，但可以支持双向遍历，带来了双向链表操作的灵活性。

### 算法题

[数组中重复的数据](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/)

```js
/* 
给定一个整数数组 a，其中 1 ≤ a[i] ≤ n（n为数组长度）, 其中有些元素出现两次而其他元素出现一次。
找到所有出现两次的元素。
你可以不用到任何额外空间并在O(n)时间复杂度内解决这个问题吗？

示例：
输入:
[4,3,2,7,8,2,3,1]
输出:
[2,3]
*/

/**
 * @param {number[]} nums
 * @return {number[]}
 */
var findDuplicates = function (nums) {
  const res = [];
  if (nums.length === 0) {
    return res;
  }

  for (const num of nums) {
    const index = Math.abs(num) - 1;
    if (nums[index] < 0) {
      res.push(Math.abs(num));
    }
    nums[index] = -nums[index];
  }
  return res;
};
```

读题真的很重要，理解题意是解答题目的关键。

因为 1 ≤ a[i] ≤ n，所以当我们遍历数组时，一定可以通过 `a[i] - 1` 为下标访问访问到数组中的某个元素，如果是第一次访问到该元素，那我们就将该元素取反，如果往后遍历中再次访问到负数元素，就说明遇到了相同元素，就将该元素存入 result，取绝对值是因为当前循环的值可能在之前被访问过取反了。

## Review

[5 CSS Practices To Avoid as a Web Developer](https://betterprogramming.pub/5-css-practices-to-avoid-as-a-web-developer-1b7553c05131)

1. Set Margins or Padding and Then Reset Them
2. Add display: block for Elements With position: absolute or position: fixed
3. Use transform: translate (-50%, -50%) To Center
4. Use width: 100% for Block Elements
5. Set display: block for Flex Items

Indeed, some of these practices are used in my projects. But when I look deeper, I see that the root cause is my deficient knowledge of CSS. For example, I didn't know the specific usage of `:nth-child`, what a shame!

### Words

* crutches：拐杖，walking with a crutches
* concise：简洁的，brief
* adjacent：two things are next to each other
* arbitrary：蛮横的，武断的，using unlimited personal power without considering other people's rights or wishes

## Tip

[修改 git commit 的 author 信息](https://cq036pgwqz.feishu.cn/docs/doccnpOOKksEOKVQmPYX11iM00b)

## Share

[从 0 开始手把手带你搭建一套规范的 Vue3.x 项目工程环境](https://juejin.cn/post/6951649464637636622)

这篇文章简直 awesome！

文章主要分为 5 个方面来介绍项目的规范化：

1. 架构搭建
2. 代码规范
3. 提交规范
4. 单元测试
5. 自动部署

这基本涵盖了前端项目开发的整个流程，特别适合刚刚接触前端工程化的同学。
