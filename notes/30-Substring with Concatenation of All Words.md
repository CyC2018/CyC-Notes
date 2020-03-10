[Leetcode](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)

## recursion + upper and lower bound

1. 这里要注意了，不是简单判断当前node比左孩子和右孩子大就行，因为会出现你在parent右子树，结果你的左孩子比你的parent还小的情况，这种情况显然是不合法的，这个坑一定要注意了，不要想简单了。
2. 所以我们用个helper函数，目的是随时记录当前的upper bound和lower bound，起始值为null，所以用Integer比较好，简单判断不是null就可以比较了。
3. 递归下去的时候往左边的话，把自己的值作为upper bound，往右边走，把自己值作为lower bound。

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return helper(root, null, null);
    }
    private boolean helper(TreeNode root, Integer lower, Integer upper) {
        if (root == null) return true;
        if (lower != null && root.val <= lower) return false;
        if (upper != null && root.val >= upper) return false;
        return helper(root.left, lower, root.val) && helper(root.right, root.val, upper);
    }
}
```
