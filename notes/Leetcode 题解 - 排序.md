<!-- GFM-TOC -->
* [快速选择](#快速选择)
* [堆](#堆)
    * [215. Kth Largest Element in an Array](#1-kth-element)
* [桶排序](#桶排序)
    * [347. Top K Frequent Elements](#1-出现频率最多的-k-个元素)
    * [451. Sort Characters By Frequency](#2-按照字符出现次数对字符串排序)
* [荷兰国旗问题](#荷兰国旗问题)
    * [75. Sort Colors](#1-按颜色进行排序)
<!-- GFM-TOC -->


# 快速选择

用于求解   **Kth Element**   问题，也就是第 K 个元素的问题。

可以使用快速排序的 partition() 进行实现。需要先打乱数组，否则最坏情况下时间复杂度为 O(N<sup>2</sup>)。

# 堆

用于求解   **TopK Elements**   问题，也就是 K 个最小元素的问题。可以维护一个大小为 K 的最小堆，最小堆中的元素就是最小元素。最小堆需要使用大顶堆来实现，大顶堆表示堆顶元素是堆中最大元素。这是因为我们要得到 k 个最小的元素，因此当遍历到一个新的元素时，需要知道这个新元素是否比堆中最大的元素更小，更小的话就把堆中最大元素去除，并将新元素添加到堆中。所以我们需要很容易得到最大元素并移除最大元素，大顶堆就能很好满足这个要求。

堆也可以用于求解 Kth Element 问题，得到了大小为 k 的最小堆之后，因为使用了大顶堆来实现，因此堆顶元素就是第 k 大的元素。

快速选择也可以求解 TopK Elements 问题，因为找到 Kth Element 之后，再遍历一次数组，所有小于等于 Kth Element 的元素都是 TopK Elements。

可以看到，快速选择和堆排序都可以求解 Kth Element 和 TopK Elements 问题。

## 1. Kth Element

215\. Kth Largest Element in an Array (Medium)

[Leetcode](https://leetcode.com/problems/kth-largest-element-in-an-array/description/) / [力扣](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/description/)

```text
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

题目描述：找到倒数第 k 个的元素。

**排序**  ：时间复杂度 O(NlogN)，空间复杂度 O(1)

```java
public int findKthLargest(int[] nums, int k) {
    Arrays.sort(nums);
    return nums[nums.length - k];
}
```

**堆**  ：时间复杂度 O(NlogK)，空间复杂度 O(K)。

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int num : nums) {
            pq.add(num);
            if (pq.size() > k) { // 维护堆的大小为 K
                pq.poll();
            }
        }
        return pq.peek();
    }
}
```

**快速选择**  ：时间复杂度 O(N)，空间复杂度 O(1)

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int left = 0, right = nums.length - 1;
        int target = nums.length - k;
        while (left < right) {
            int piv = partition(nums, left, right);
            if (piv == target) break;
            else if (piv < target) left = piv + 1;
            else right = piv - 1;
        }
        return nums[target];
    }
    
    private int partition(int[] nums, int left, int right) {
        int pVal = nums[right];
        int leftwall = left;
        for (int i = left; i < right; i++) {
            if (nums[i] < pVal) {
                swap(nums, i, leftwall);
                leftwall++;
            }
        }
        swap(nums, right, leftwall);
        return leftwall;
    }
    
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

# 桶排序

## 1. 出现频率最多的 k 个元素

347\. Top K Frequent Elements (Medium)

[Leetcode](https://leetcode.com/problems/top-k-frequent-elements/description/) / [力扣](https://leetcode-cn.com/problems/top-k-frequent-elements/description/)

```html
Given [1,1,1,2,2,3] and k = 2, return [1,2].
```

设置若干个桶，每个桶存储出现频率相同的数。桶的下标表示数出现的频率，即第 i 个桶中存储的数出现的频率为 i。

把数都放到桶之后，从后向前遍历桶，最先得到的 k 个数就是出现频率最多的的 k 个数。

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> count = new HashMap<>();
        // 使用字典，统计每个元素出现的次数，元素为键，元素出现的次数为值
        for (int num : nums) count.put(num, count.getOrDefault(num, 0) + 1);
        // 桶排序
        // 将频率作为数组下标，对于出现频率不同的数字集合，存入对应的数组下标
        List<Integer>[] arr = new List[nums.length + 1];
        for (int key : count.keySet()) {
            if (arr[count.get(key)] == null) arr[count.get(key)] = new ArrayList<>();
            arr[count.get(key)].add(key);
        }
        // 倒序遍历数组获取出现顺序从大到小的排列
        List<Integer> res = new ArrayList<>();
        for (int i = arr.length - 1; i >= 0 && res.size() < k; i--) {
            if (arr[i] != null) res.addAll(arr[i]); 
        }
        return res;
    }
}
```

其他解法，维护一个大小为k的最小堆：

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> count = new HashMap<>();
        for (int num : nums) count.put(num, count.getOrDefault(num, 0) + 1);
        PriorityQueue<Integer> heap = new PriorityQueue<>((a, b) -> (count.get(a) - count.get(b)));
        for (int val : count.keySet()) {
            heap.add(val);
            if (heap.size() > k) {
                heap.poll();
            }
        }
        List<Integer> res = new ArrayList<>();
        while (!heap.isEmpty()) {
            res.add(heap.poll());
        }
        return res;
    }
}
```

## 2. 按照字符出现次数对字符串排序

451\. Sort Characters By Frequency (Medium)

[Leetcode](https://leetcode.com/problems/sort-characters-by-frequency/description/) / [力扣](https://leetcode-cn.com/problems/sort-characters-by-frequency/description/)

```html
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

```java
class Solution {
    public String frequencySort(String s) {
        if (s == null || s.length() == 0) return "";
        // 用哈希表计数
        HashMap<Character, Integer> count = new HashMap<>();
        for (char c : s.toCharArray()) count.put(c, count.getOrDefault(c, 0) + 1);
        // 桶排序，根据频率把字符放入相应桶中
        List<Character>[] arr = new List[s.length() + 1];
        for (char key : count.keySet()) {
            if (arr[count.get(key)] == null) arr[count.get(key)] = new ArrayList<>();
            arr[count.get(key)].add(key);
        }
        // 将字符按频率从高到低存入结果中
        StringBuilder res = new StringBuilder();
        for (int i = arr.length - 1; i >= 0; i--) {
            if (arr[i] != null) {
                for (char c : arr[i]) {
                    for (int j = 0; j < count.get(c); j++) {
                        res.append(c);
                    }
                }
            }
        }
        return res.toString();
    }
}
```

其他解法，维护一个最大堆：

```java
class Solution {
    public String frequencySort(String s) {
        if (s == null || s.length() == 0) return "";
        // 哈希表计数
        HashMap<Character, Integer> count = new HashMap<>();
        for (char c : s.toCharArray()) count.put(c, count.getOrDefault(c, 0) + 1);
        // 根据哈希表中的计数值建立字符的最大堆
        PriorityQueue<Character> heap = new PriorityQueue<>((a, b) -> (count.get(b) - count.get(a)));
        for (char key : count.keySet()) heap.add(key);
        // 频率从大到小将字符存入答案中
        StringBuilder res = new StringBuilder();
        while (!heap.isEmpty()) {
            char c = heap.poll();
            for (int i = 0; i < count.get(c); i++) {
                res.append(c);
            }
        }
        return res.toString();
    }
}
```

# 荷兰国旗问题

荷兰国旗包含三种颜色：红、白、蓝。

有三种颜色的球，算法的目标是将这三种球按颜色顺序正确地排列。它其实是三向切分快速排序的一种变种，在三向切分快速排序中，每次切分都将数组分成三个区间：小于切分元素、等于切分元素、大于切分元素，而该算法是将数组分成三个区间：等于红色、等于白色、等于蓝色。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/7a3215ec-6fb7-4935-8b0d-cb408208f7cb.png"/> </div><br>

三向切分（fast 3-way partitioning)解释文章：

https://blog.csdn.net/a8336675/article/details/51818743


## 1. 按颜色进行排序

75\. Sort Colors (Medium)

[Leetcode](https://leetcode.com/problems/sort-colors/description/) / [力扣](https://leetcode-cn.com/problems/sort-colors/description/)

```html
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

题目描述：只有 0/1/2 三种颜色。

三向切分适用于重复数很多的情况下，只要pVal中轴数选的好，能大幅减少快速排序递归下去的排序区间（其实就是减去了中间等于中轴数的部分，那部分不用再去递归排序了），实际上相当于快速排序O(NlogN)的剪枝算法，要比快速排序在大量重复数情况下快一点。

```java
class Solution {
    public void sortColors(int[] nums) {
        sortColors(nums, 0, nums.length - 1);
    }
    
    private void sortColors(int[] nums, int left, int right) {
        if (left >= right) return;
        int leftwall = left, rightwall = right, cur = leftwall + 1, pVal = nums[leftwall];
        while (cur <= rightwall) {
            if (nums[cur] < pVal) {
                swap(nums, cur, leftwall);
                cur++;
                leftwall++;
            } else if (nums[cur] > pVal) {
                swap(nums, cur, rightwall);
                rightwall--;
            } else {
                cur++;
            }
        }
        sortColors(nums, left, leftwall - 1);
        sortColors(nums, rightwall + 1, right);
    }
    
    private void swap(int[] nums, int i, int j) {
        int t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
    }
}
```

这题要利用数组中只有三个数的特点，把三向切分变种一下，实现O(N)时间复杂度。

```java
public void sortColors(int[] nums) {
    int zero = -1, one = 0, two = nums.length;
    while (one < two) {
        if (nums[one] == 0) {
            swap(nums, ++zero, one++);
        } else if (nums[one] == 2) {
            swap(nums, --two, one);
        } else {
            ++one;
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int t = nums[i];
    nums[i] = nums[j];
    nums[j] = t;
}
```






<div align="center"><img width="320px" src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/githubio/公众号二维码-2.png"></img></div>
