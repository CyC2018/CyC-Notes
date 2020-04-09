<!-- GFM-TOC -->
* [452. Minimum Number of Arrows to Burst Balloons](https://github.com/yhx89757/CS-Notes/blob/master/notes/452.%20Minimum%20Number%20of%20Arrows%20to%20Burst%20Balloons.md)
* [435. Non-overlapping Intervals](https://github.com/yhx89757/CS-Notes/blob/master/notes/435.%20Non-overlapping%20Intervals.md)
* [56. Merge Intervals](https://github.com/yhx89757/CS-Notes/blob/master/notes/56.%20Merge%20Intervals.md)
* [763. Partition Labels](https://github.com/yhx89757/CS-Notes/blob/master/notes/763.%20Partition%20Labels.md)
* [57. Insert Interval](https://github.com/yhx89757/CS-Notes/blob/master/notes/57.%20Insert%20Interval.md)
* [986. Interval List Intersections](https://github.com/yhx89757/CS-Notes/blob/master/notes/986.%20Interval%20List%20Intersections.md)
* [729. My Calendar I](https://github.com/yhx89757/CS-Notes/blob/master/notes/729.%20My%20Calendar%20I.md)
* [218. The Skyline Problem](https://github.com/yhx89757/CS-Notes/blob/master/notes/218.%20The%20Skyline%20Problem.md)
* [252. Meeting Rooms](https://github.com/yhx89757/CS-Notes/blob/master/notes/252.%20Meeting%20Rooms.md)
* [253. Meeting Rooms II](https://github.com/yhx89757/CS-Notes/blob/master/notes/253.%20Meeting%20Rooms%20II.md)
* [759. Employee Free Time](#4-我的日程安排表1)
* [495. Teemo Attacking](https://github.com/yhx89757/CS-Notes/blob/master/notes/495.%20Teemo%20Attacking)
* [616. Add Bold Tag in String](#4-我的日程安排表1)
* [715. Range Module](#4-我的日程安排表1)
* [436. Find Right Interval](https://github.com/yhx89757/CS-Notes/blob/master/notes/436.%20Find%20Right%20Interval.md)
* [352. Data Stream as Disjoint Intervals](https://github.com/yhx89757/CS-Notes/blob/master/notes/352.%20Data%20Stream%20as%20Disjoint%20Intervals.md)
<!-- GFM-TOC -->

https://zhuanlan.zhihu.com/p/90664857

https://zhuanlan.zhihu.com/p/26657786

leetcode大神总结模板：

https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/discuss/93735/A-Concise-Template-for-%22Overlapping-Interval-Problem%22

重叠区间问题可以总结为在坐标轴上若干个位置为 (start(i),end(i))的区间，要求求解这些区间中有多少个不重叠区间，或者合并重叠的区间。

该问题分两类：第一类求不重叠区间个数（leetcode 452，435），第二类求合并后的区间（leetcode 56，763）。

对于第一类问题，通常按照end排序，维护一个end变量即可。

对于第二类问题，通常按照start排序，维护一个数组，每次取最后一个数作为比较的标准。

注意按照start或者end排序两种方式都可以求解，只是在不同情况下用其中之一代码编写更简洁。
