# week_007

## Algorithm

### 算法题

[两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

```js
/*
题目：给你两个 非空 的链表，表示两个非负的整数。它们的每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。
请你将两数相加，并以相同形式返回一个表示和的链表。
你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例一：
输入：l1 = [2, 4, 3], l2 = [5, 6, 4]
输出：[7, 0, 8]
解释：342 + 465  = 807

示例二：
输入：l1 = [0], l2 = [0]
输出：[0]

示例三：
输入：l1 = [9, 9, 9, 9, 9, 9, 9], l2 = [9, 9, 9, 9]
输出：[8, 9, 9, 9, 0, 0, 0, 1]
*/

/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
// ❌ 错误解法：将链表和数组混淆
var addTwoNumbers = function (l1, l2) {
  let res = null;

  const resNum = Number(l1.reverse().join('')) + Number(l2.reverse().join(''))

  const arrStr = (resNum + '').split('').reverse()

  res = arrStr.map(str => Number(str))

  return res;
};
// 解法一：
var addTwoNumbers = function (l1, l2) {
  let head = null, tail = null;
  let carry = 0;
  while (l1 || l2) {
    const n1 = l1 ? l1.val : 0;
    const n2 = l2 ? l2.val : 0;
    const sum = n1 + n2 + carry;
    if (!head) {
      head = tail = new ListNode(sum % 10);
    } else {
      tail.next = new ListNode(sum % 10);
      tail = tail.next;
    }
    carry = Math.floor(sum / 10);
    if (l1) {
      l1 = l1.next;
    }
    if (l2) {
      l2 = l2.next;
    }
  }
  if (carry > 0) {
    tail.next = new ListNode(carry);
  }
  return head;
};
```

## Review

[Understanding Closures in JavaScript](https://cq036pgwqz.feishu.cn/docs/doccnKgjHK720JIGRrr8RssTGcM)

## Tip

[JS 中的防抖和节流](https://cq036pgwqz.feishu.cn/docs/doccnbA4ov59TrbRMDPctId37y6)

## Share

[《JavaScript 二十年》](https://github.com/doodlewind/jshistory-cn)

> 这本书是由 JavaScript 之父 Brendan Eich 与 ES6 规范首席作者 Allen Wirfs-Brock 联合编写，书中详细记载和解读了自1995 年语言诞生到 2015 年 ES6 规范制定为止，共计 20 年的 JavaScript 语言演化历程。全书不仅讲解了大量语言技术细节层面的演进，更复盘了更高层面上规范制定与标准博弈中的历史成败，是一部讲述人类如何在商业与技术上的竞争合作中促进产业发展的故事。

之前在线上看过部分，觉得写得挺好，便买了纸质书，最近正在看，书中的细节还是蛮丰富的，推荐！
