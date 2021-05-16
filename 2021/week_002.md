# week_002

## Algorithm

### 数据结构-数组（Array）

最基础的数据结构。

为什么数组要从 0 开始编号，而不是从 1 开始？

数组是一种**线性表数据结构**。它用**一组连续的内存空间**，来存储一组具有相同类型的数据。

> [为什么在 JavaScript 中，数组可以保存不同类型的数据呢？](https://segmentfault.com/a/1190000037627661)

* 线性表（Linear List）：数据排成一条线一样的结构，线性表上的数据只有前和后两个方向（链表、队列、栈等）。
* 非线性表：数据不是简单的前后关系（二叉树、堆、图等）。

连续的内存空间和相同类型的数据带来的优缺点：

* 优点：随机访问
* 缺点：删除、插入数据时，为了保证连续性，需要做大量数据搬移工作，低效。

数组如何实现根据下标随机访问数组元素，数组寻址公式：

```bash
# int[] a = new int[10]，内存块首地址为 base_address = 1000
# 计算机会给每个内存单元分配地址，通过地址来访问内存中的数据
a[i]_address = base_address + i * data_type_size
# i 为下标，data_type_size 表示数组中每个元素的大小
```

数组是适合查找操作，但是查找的时间复杂并不为 O(1)，即便是拍好序的数组，使用二分查找，时间复杂度也是 O(logn)。正确的表述应该是，数组支持随机访问，根据下标随机访问的时间复杂度为 O(1)。

#### 低效的“插入”和“删除”

为何低效？

因为数组为了保持内存数据的连续性。

当插入操作时，正常往一个长度为 n 的数组的第 k 位里插入一个数据，最好时间复杂度为 O(1)（在末尾插入），最坏时间复杂度为 O(n)（在第一位插入），所以平均时间复杂度为 O(n)。

当删除操作时，从长度位 n 的数组中删除第 k 位数据，为了保证内存的连续性，也需要搬移数据，不然中间会出现空洞，内存不连续。同理，最好时间复杂度为 O(1)，最坏时间复杂度为 O(n)，平均时间复杂度为 O(n)。

如何解决？

* 插入：把第 k 位数据搬移到数组最后，新数据放入第 k 位。
* 删除：标记清除。

#### 数组越界访问问题

访问数组的本质是访问一段连续的内存，只要数组通过偏移计算得到的内存地址是可用的，那么程序就可能不会报任何错误。

#### 解答数组从 0 开始编号

从数组存储的内存模型上来看，“下标”最确切的定义应该是“偏移（offset）”。再来看看我们的寻址公式：

```bash
a[k]_address = base_address + k * type_size
```

如果从 1 开始编号，那么寻址公式将会变成：

```bash
a[k]_address = base_address + (k - 1) * type_size
```

可以发现，从 1 开始编号，每次随机访问数组都多了一次减法运算。但主要还是历史原因。

### 算法题

[两个数组的交集](https://www.geekxh.com/1.0.%E6%95%B0%E7%BB%84%E7%B3%BB%E5%88%97/001.html#_01%E3%80%81%E9%A2%98%E7%9B%AE%E5%88%86%E6%9E%90)

```js
/*
给定两个数组，编写一个函数计算它们的交集。

示例 1：

输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2,2]

示例 2：

输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [4,9]
*/
```

## Review

## Tip

[JavaScript 执行机制 in 浏览器](https://cq036pgwqz.feishu.cn/docs/doccn32aWiEGYWbpu5jPxqTt3le?from=from_copylink)

## Share

[你真的了解js数组吗？](https://segmentfault.com/a/1190000037627661)

这周跟着极客时间里王争老师的《数据结构和算法之美》课程学习了关于数组相关的知识，发现自己对于这个编程中最常用的数据结构之一，还是知之甚少，也对 JavaScript 中的数组有了一些新的理解和思考。

在对于数组的定义中提到一点，数组用一组连续的内存空间，来存储一组具有相同类型的数据。但是在 JS 中，数组中存储的数据可以不是相同的类型。

```js
let arr = [1, 'string', {name: 'whh'}, function hello() {}]
```

此时我就陷入了疑惑，怎么 JS 的数组表现还和数组的定义冲突了呢？

其实这里我陷入一个误区，就是对数据结构和数据类型理解有误，所以就有必要先弄清楚这两个概念。

A data structure is a way of describing a certain way to organize peices of data so that operations and algorithms can be more easily applied.

A data type describes a peices of data that all share a common property. For example an integer data type describes every integer the computer can handle.

所以说，数据结构中所指的数组和 JS 语言中所定义的数据类型数组其实是两个东西。

### JS 中，数组为什么可以保存不同类型？

```c++
// The JSArray describes JavaScript Arrays 
//  Such an array can be in one of two modes: 
//    - fast, backing storage is a FixedArray and length <= elements.length(); 
//       Please note: push and pop can be used to grow and shrink the array. 
//    - slow, backing storage is a HashTable with numbers as keys. 
class JSArray: public JSObject {  
    public: // [length]: The length property. 
        DECL_ACCESSORS(length, Object)  
    // ...此处省略实现  
    // Number of element slots to pre-allocate for an empty array. 
    static const int kPreallocatedArrayElements = 4; 
};
```

如上我们可以看出 JSArray 是继承自 JSObject 的，所以在 JavaScript 中，数组可以是一个特殊的对象，内部也是以 key-value 形式存储数据，所以 JavaScript 中的数组可以存放不同类型的值。

### JS 数组的增删改查

#### 增加

```js
let arr = ['a']

// 通过 push 方法向尾部添加
arr.push('b')

// 通过 length 属性向尾部添加
arr[arr.length] = 'c'

// 通过 unshift 方法向头部添加
arr.unshift('0')

// 通过 contact 拼接数组
arr.concat(['d', 'e'])

// 通过 splice 向任意位置添加数据
arr.splice(1, 0, 'f', 'g')
```

#### 删除和修改

```js
// 通过 shift 方法从头部删除
arr.shift()

// 通过 pop 方法从尾部删除
arr.pop()

// 通过 splice 方法删除指定 index 的 item
arr.splice(index, deleteCount)

// 通过 slice shallow copy 返回新数组
arr.slice(0, 1)

// 通过 filter 获取符合条件新数组
arr.filter(item => item.id > 33)
```

#### 查找及其他

```js
let arr = [1, 2, 3]

arr.toString() // '1, 2, 3'
arr.join('-') // '1-2-3'
arr.sort()
...
```
