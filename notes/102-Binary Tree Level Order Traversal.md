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
