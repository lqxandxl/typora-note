## 513 找树的左下角的值

请找出该二叉树的 最底层 最左边 节点的值。

使用dfs走到深度最深的位置，第一次的时候就是最左边的。需要在边dfs的时候边记录深度。

```
class Solution {
    public int maxDepth = 0;
    public int ans = -1;
    public int findBottomLeftValue(TreeNode root) {
        maxDepth = 0;
        ans = -1;
        dfs(root,0);
        return ans;
    }

    public void dfs(TreeNode root,int depth){
        if(root==null)
            return;
        depth = depth + 1;
        if(depth > maxDepth){
            ans = root.val;
            maxDepth = depth;
        }
        dfs(root.left,depth);
        dfs(root.right,depth);
    }
}
```

