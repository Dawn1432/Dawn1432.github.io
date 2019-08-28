---
layout: post
title: 刷题笔记-leetcode 
date: 2019-08-12
tags: brushing_crazily
---
### 概述
在这个磨皮擦痒的值班日，终于是可以在公司正当地干点自己期望的事情了。最近受“马奇利”台风影响，上班是穿着雨衣来的，为了避免电脑被打湿这类的不必要的麻烦也就没有把笔记本带来，否则这种时候我肯定在研究我博客上看板娘的事情。看板娘也是最近才加的，也算是给起灰的博客搞了点动静。
所以终于想起来好几个朋友都推荐我去试试leetcode的编程题，这里面都是一些经典的编程题目。于是打开牛客网，打开在线编程，翻了几道看起来比较容易的题目，开始把算法研究的工作再捡起来。
## 正文
### <font size="2">2019-08-10 ： 3/148</font>
<p>
1、经典题目：边数边说。<br>
The count-and-say sequence is the sequence of integers beginning as follows:<br>
1, 11, 21, 1211, 111221, ...<br>
1is read off as"one 1"or11.<br>
11is read off as"two 1s"or21.<br>
21is read off as"one 2, thenone 1"or1211.<br>
Given an integer n, generate the n th sequence.<br>
</p>
<p>
所实话，题干比题目本身难...<br>
从1开始，数上一个数列中每个数字出现了几次，把count+number这样排列形成下一个数列。<br>
但是看到111221的时候突然懵逼了，1211的下一个不应该是3112吗？<br>
其实这里的次数不是整个数列出现的次数，到不同的数字为止，分段来数的，所以1211，应该这么数，[1][2][11]。<br>
然后思路就是逐个扫描数个数，到不同数字的为止。<br>
</p>
2/3、经典题目：二叉树的最小深度/最大深度<br>
可以说这两个逻辑是一致的，就是一个大于/小于的区别。<br>
我先做的最大深度，思路如下：<br>
（1）该节点是否为空，是则返回0；否则继续。<br>
（2）该节点的左子节点是否存在，存在则递归计算左子节点的最大深度；不存在则继续。<br>
（3）该节点的右子节点是否存在，存在则递归计算右子节点的最大深度；不存在则继续。<br>
（4）最后比较左子节点和右子节点的最大深度，返回最大的那个+1。<br>
代码如下：<br>
```java
public int maxDepth(TreeNode root) {
	if (null == root) {
		return 0;
	}
	int leftDepth = 0;
	if (null != root.left) {
		leftDepth = maxDepth(root.left);
	}
	int rightDepth = 0;
	if (null != root.right) {
		rightDepth = maxDepth(root.right);
	}
	return (leftDepth > rightDepth ? leftDepth : rightDepth) + 1;
}
```
一次AC，牛逼。<br>
好，改了一个符号提交第二道题，二叉树的最小深度。<br>
<img src='https://dawn1432.github.io\images\刷题笔记-leet_code\不通过.png' align='margin-left' style=' width:500px;height:150px;margin:0;'/><br>
<img src='https://dawn1432.github.io\images\刷题笔记-leet_code\what.jpg' align='margin-left' style=' width:150px;height:150px;margin:0;'/><br>
百思不得其解，于是看了别人提交的答案，于是有了第二种思路：<br>
（1）该节点是否为空，是则返回0；否则继续。<br>
（2）该节点的左子节点是否存在，不存在则返回右子节点的最小深度+1。<br>
（3）该节点的右子节点是否存在，不存在则返回左子节点的最小深度+1。<br>
（4）如果左右节点都存在，则返回左右子节点最小深度结果中最小的那个+1。<br>
代码如下：<br>
```java
public int run(TreeNode root) {
	if (null == root) {
		return 0;
	}
	if (null == root.left) {
		return run(root.right) + 1;
	}
	if (null == root.right) {
		return run(root.left) + 1;
	}
	return Math.min(run(root.left), run(root.right)) + 1;
}
```
使用了逆向思维，排除着进行计算，骚是骚了点，但是这难道跟我的思路有很大区别吗？？？
<img src='https://dawn1432.github.io\images\刷题笔记-leet_code\有什么区别.png' align='margin-left' style=' width:150px;height:150px;margin:0;'/><br>
### <font size="2">2019-08-28 ： 8/148</font>
4、后缀表达式
经常出现在选择题中的存在，一般让你判断后缀表达式对不对，或者计算结果是多少。<br>
反正能想到使用栈（Stack）就差不多了，这次实际用代码体验了一下：<br>
（1）列表中的符号数字依次扔入栈中。<br>
（2）从栈中拿出一个，判断是哪个符号。<br>
（3）再依次拿出操作值和被操作值。（如果拿到的是符号，递归计算出该值。）<br>
（4）从第（2）步开始循环，直到栈为空。
5、在O(n log n)的时间内使用常数级空间复杂度对链表进行排序。<br>
对链表的排序方法多种多样，但是限制了时间和空间复杂度，那很明显（看完讨论后）基本确定使用归并法了。参照之前提到过的：[排序与查找](https://dawn1432.github.io/2018/10/sort&find/)<br>
也是第一次体验归并法：<br>
（1）快慢指针找中点，并从该点切断链表。<br>
（2）递归执行前半部分的排序。<br>
（3）递归执行后半部分的排序。<br>
（4）合并两部分排序结果。<br>
这里在思路出来后，在切断的部分用单指针想了半天，但是最后还是需要双指针来解决。（自己思维太僵硬）<br>
6、孤独的数字<br>
<img src='https://dawn1432.github.io\images\刷题笔记-leet_code\展博念诗.png' align='margin-left' style=' width:150px;height:150px;margin:0;'/><br>
现在有一个整数类型的数组，数组中素只有一个元素只出现一次，其余的元素都出现两次。<br>
注意：<br>
你需要给出一个线性时间复杂度的算法，你能在不使用额外内存空间的情况下解决这个问题么？<br>
Given an array of integers, every element appears twice except for one. Find that single one.<br>
Note: <br>
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?<br>
看完题干，感觉问题不大；看完注意，时间复杂度O(n)，空间复杂度0，陷入沉思...<br>
<img src='https://dawn1432.github.io\images\刷题笔记-leet_code\思考.gif' align='margin-left' style=' width:50px;height:50px;margin:0;'/><br>
<img src='https://dawn1432.github.io\images\刷题笔记-leet_code\a few moments later.jpg' align='margin-left' style=' width:170px;height:100px;margin:0;'/><br>
那很明显（看完讨论后），把每个值依次进行异或，结果就是那个孤独的值。看完之后，叹为观止。<br>
7、二叉树的后序遍历。<br>
递归的思路很简单，递归完左边，递归右边，最后输出该节点。<br>
但这道题让你用迭代的方式来做...再次陷入沉思...<br>
思考（百度）过后，得到了一个非常不错的迭代遍历二叉树灵感：<br>
（1）提前将根节点入栈。<br>
（2）然后选取栈顶元素进行迭代，判断当前节点是否存在子节点；若存在右子节点，将右子节点入栈；若存在左子节点，将做子节点入栈；（注意先入栈右后左，出栈时才符合先左后右的顺序）。<br>
（3）如果当前节点不存在子节点；弹出栈顶，并输出。直到当前节点为空或者栈为空为止。<br>
想得很美好，但是弹着弹着发现，回到父节点后，由于父节点存在子节点，子节点又入栈了...，从此无限循环<br>
所以这里需要添加一个限制<br>
（4）若果节点的子节点都遍历过了，那么该节点等同于没有子节点；翻译一些就是，如果刚弹出去那个节点是当前栈顶节点的子节点的时候，弹出栈顶，并输出。与（3）的逻辑相同。<br>
在代码中初始化了一个为null的pre来记录刚刚弹出的节点。由于在刚开始时pre = null，在迭代到只有左/右节点的情况时会导致进入（4）的逻辑提前输出，所以必须限制pre != null<br>
所以核心的逻辑就成了下面这样：<br>
```java
TreeNode cur = root;
stack.push(cur);
TreeNode pre = null;
while (cur != null || !stack.isEmpty()) {
	if ((cur.left == null && cur.right == null) || (pre != null && (pre == cur.left || pre == cur.right))) {
		pre = stack.pop();
		result.add(pre.val);
	} else {
		if (cur.right != null) {
			stack.push(cur.right);
		}
		if (cur.left != null) {
			stack.push(cur.left);
		}
	}
	cur = stack.peek();
}
```
8、穷举算法<br>
对于给定的n个位于同一二维平面上的点，求最多能有多少个点位于同一直线上<br>
Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.<br>
这个题放给任何一个初中生都有思路，可以计算所有点是否属于同于个一元二次函数...。<br>
但是写程序的话这么想就太僵硬了，截距怎么算？斜率算下来除不尽怎办？有根号怎么办？一个个问题困扰着我，拉我陷入沉思（入眠）<br>
<img src='https://dawn1432.github.io\images\刷题笔记-leet_code\入眠.jpg' align='margin-left' style=' width:50px;height:50px;margin:0;'/><br>
沉思（看过讨论）过后，总结了一下思路：<br>
1、双重循环给所有点配对，每次配对固定一个源点，遍历其他所有点。【这样就不用考虑截距，斜率相同即共线】<br>
2、用分数表达斜率，避免除法除不尽产生误差。<br>
3、分子分母同时除以最大公约数，以达到约分效果。【比较斜率是否相同时，需要比对分数以及正负】<br>
4、使用辗转相除法计算最大公约数。<br>
5、[使用异或实现辗转中的数值交换](https://dawn1432.github.io/2018/11/sort&find;Easy-sorting/)。<br>
注意特殊情况：<br>
1、所以分子为0的斜率直接判定为共线。<br>
2、所有分母为0的斜率直接判定为共线。<br>
3、每存在一对点重合时，当前所有的线条上的共线点数加1。<br>
