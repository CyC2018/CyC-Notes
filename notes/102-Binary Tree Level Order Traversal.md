[Leetcode](https://leetcode.com/problems/binary-tree-level-order-traversal/)

## queue

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode cur = queue.poll();
                if (cur.left != null) queue.add(cur.left);
                if (cur.right != null) queue.add(cur.right);
                list.add(cur.val);
            }
            res.add(list);
        }
        return res;
    }
}
```

## recursion

下面我们来看递归的解法，由于递归的特性，我们会一直深度优先去处理左子结点，那么势必会穿越不同的层，所以当要加入某个结点的时候，我们必须要知道当前的深度，所以使用一个变量level来标记当前的深度，初始化带入0，表示根结点所在的深度。由于需要返回的是一个二维数组res，开始时我们又不知道二叉树的深度，不知道有多少层，所以无法实现申请好二维数组的大小，只有在遍历的过程中不断的增加。那么我们什么时候该申请新的一层了呢，当level等于二维数组的大小的时候，为啥是等于呢，不是说要超过当前的深度么，这是因为level是从0开始的，就好比一个长度为n的数组A，你访问A[n]是会出错的，当level等于数组的长度时，就已经需要新申请一层了，我们新建一个空层，继续往里面加数字，参见代码如下：

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        levelOrder(root, 0, res);
        return res;
    }
    private void levelOrder(TreeNode root, int level, List<List<Integer>> res) {
        if (root == null) return;
        if (res.size() == level) res.add(new ArrayList<>());
        res.get(level).add(root.val);
        if (root.left != null) levelOrder(root.left, level + 1, res);
        if (root.right != null) levelOrder(root.right, level + 1, res);
    }
}
```
