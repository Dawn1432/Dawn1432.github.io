---
layout: post
title: 刷题笔记-leet code 
date: 2018-11-16
tags: brushing_crazily
---
### 概述
在这个磨皮擦痒的值班日，终于是可以在公司正当地干点自己期望的事情了。最近受“马奇利”台风影响，上班是穿着雨衣来的，为了避免电脑被打湿这类的不必要的麻烦也就没有把笔记本带来，否则这种时候我肯定在研究我博客上看板娘的事情。看板娘也是最近才加的，也算是给起灰的博客搞了点动静。
所以终于想起来好几个朋友都推荐我去试试leetCode的编程题，这里面都是一些经典的编程题目。于是打开牛客网，打开在线编程，翻了几道看起来比较容易的题目，开始把算法研究的工作再捡起来。
## 正文
### <font size="2">2019-8-10 ： 3/148</font>
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
2、经典题目：二叉树的最小深度/最大深度<br>
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