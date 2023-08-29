# 剑指 Offer 32 - I. 从上到下打印二叉树


## 解题思路

* 二叉树的层序遍历


```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] levelOrder(TreeNode root) {
        // 二叉树的层序遍历
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        // if(root == null){
        //     return new int[];
        // }

        List<Integer> list = new ArrayList<>();

        while(!q.isEmpty()){
            int size = q.size();
            for(int i = 0; i < size; i++){
                TreeNode cur =  q.poll();
                if(cur != null){
                     list.add(cur.val);
                     if(cur.left != null){
                    q.offer(cur.left);
                }

                    if(cur.right != null){
                        q.offer(cur.right);
                    }
                }
                
            }
        }

        // 将list转换为数组
        int[] r = new int[list.size()];

        int i  = 0;
        for(int num:list){
            r[i++] = num;
        }
        return r;
    }
}

```