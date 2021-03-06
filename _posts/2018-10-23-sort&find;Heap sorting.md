---
layout: post
title: 堆排序
date: 2018-10-23
tags: sort&find
---

### 堆排序

ask:啥是堆(heap)?
- 堆是一棵完全二叉树。(啥是完全二叉树？(￣ε(#￣)☆╰╮o(￣皿￣///))
- 堆中的节点的值总是≥或≤其左右子节点的值。
<font size="1">大于等于左右子节点，称为<strong>大顶堆</strong>，一般用于<strong>升序</strong>;
<br>小于等于左右子节点，称为<strong>小顶堆</strong>，一般用于<strong>降序</strong>。</font> 
ask:但是我们一般排序都是用的数组啊？
- 一般按层进行编号，并映射到数组中。
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆编号.png' align='margin-left' style=' width:400px;height:400px;margin:0;'/><br>
然后，通过一个例子来讲一下堆排序的主要步骤：<br>
有一个数组要求进行升序排序：70 4 44 86 68 96 76 26 ;<br>
第一步，转成初始堆；<br>
(1)转换成初始完全二叉树；
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始化完全二叉树.png' align='margin-left' style=' width:400px;height:400px;margin:0;'/><br>
(2)从叶节点开始，修正与其父节点的大小关系；（大顶堆）<br>
ask:怎么修正？<br>
- a)从当前节点的父节点开始，选择其左子节点，右子节点和自身三个值中最大的放到当前位置；
- b)如果发生交换，则继续迭代判断交换的位置；
- c)迭代完成后继续判断同层的下一个非叶子节点；
- d)当前层全部判断完成后上升一层继续判断；<br>
那上面的例子就是：（红色是当前指针位置，深蓝色是发现有可以交换的节点）
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-1.png' align='margin-left' style=' width:350px;height:350 px;margin:0;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-2-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-2.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-3-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-3.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-4-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-4.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-5-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\初始堆整理-5.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
好了，初始堆构造完成。
<hr>
第二步，首先将待排序数组分为无序和有序两个区域，然后将无序区的第一个值与无序区最后一个值交换，然后把无序区最末尾一个值划为有序区，然后把新的无序区进行修正；<font color="#FF0000" size="1"><strong>(此时直接从顶点开始修正，因为除了顶点外，其他都是符合大顶堆条件的节点)</strong></font><br>

(1)首尾交换；
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\首尾交换-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
(2)堆整理；<br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环1-1-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环1-1.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环1-2-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环1-2.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<hr>
然后循环执行第二步，直到无序区为空，则有序区排序完成。
第二次循环：<br>
(1)首尾交换；
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\首尾交换-1.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
(2)堆整理；<br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环2-1-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环2-1.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<hr>
第三次循环：<br>
(1)首尾交换；
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\首尾交换-2.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
(2)堆整理；<br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环3-1-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环3-1.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<hr>
第四次循环：<br>
(1)首尾交换；
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\首尾交换-3.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
(2)堆整理；<br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环4-1-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环4-1.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环4-2-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环4-2.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<hr>
第五次循环：<br>
(1)首尾交换；
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\首尾交换-4.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
(2)堆整理；<br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环5-1-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环5-1.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<hr>
第六次循环：<br>
(1)首尾交换；
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\首尾交换-5.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
(2)堆整理；<br>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环6-1-0.png' align='margin-left' style=' width:350px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\箭头.png' align='margin-left' style=' width:50px;height:350px;margin:0;float:left;'/>
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\堆整理循环6-1.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/>
<hr>
第七次循环：<br>
(1)首尾交换；
<img src='https://dawn1432.github.io\images\排序与查找\堆排序\首尾交换-6.png' align='margin-left' style=' width:350px;height:350px;margin:0;'/><br>
(2)堆整理；
<br>
无
<br>其实这里剩最后一个的时候就已经有序了。