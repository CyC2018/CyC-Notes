<!-- GFM-TOC -->
* [452. Minimum Number of Arrows to Burst Balloons](#4-我的日程安排表1)
* [435. Non-overlapping Intervals](#4-我的日程安排表1)
* [56. Merge Intervals](#1-合并区间)
* [763. Partition Labels](#4-我的日程安排表1)
* [57. Insert Interval](#2-插入区间)
* [986. Interval List Intersections](#3-区间列表的交集)
* [729. My Calendar I](#4-我的日程安排表1)
* [218. The Skyline Problem](#4-我的日程安排表1)
* [252. Meeting Rooms](#4-我的日程安排表1)
* [253. Meeting Rooms II](#4-我的日程安排表1)
* [759. Employee Free Time](#4-我的日程安排表1)
* [495. Teemo Attacking](#4-我的日程安排表1)
* [616. Add Bold Tag in String](#4-我的日程安排表1)
* [715. Range Module](#4-我的日程安排表1)
* [436. Find Right Interval](#4-我的日程安排表1)
* [352. Data Stream as Disjoint Intervals](#4-我的日程安排表1)
<!-- GFM-TOC -->

https://zhuanlan.zhihu.com/p/90664857

https://zhuanlan.zhihu.com/p/26657786

leetcode大神总结模板：

https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/discuss/93735/A-Concise-Template-for-%22Overlapping-Interval-Problem%22

重叠区间问题可以总结为在坐标轴上若干个位置为 (start(i),end(i))的区间，要求求解这些区间中有多少个不重叠区间，或者合并重叠的区间。

该问题分两类：第一类求重叠区间个数（leetcode 452，435），第二类求合并后的区间（leetcode 56，763）。

对于第一类问题，通常按照end排序，维护一个end变量即可。

低于第二类问题，通常按照start排序，维护一个数组，每次取最后一个数作为比较的标准。

注意按照start或者end排序两种方式都可以求解，只是在不同情况下用其中之一代码编写更简洁。
