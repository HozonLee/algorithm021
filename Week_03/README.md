学习笔记

#作业提交格式
＃学号: G20200343180026  
＃姓名:李超群  
＃班级:21期  
＃语言:Java  
＃作业链接:https://github.com/HozonLee/algorithm021/tree/main/Week_03  
＃总结链接:https://github.com/HozonLee/algorithm021/tree/main/Week_03/README.md

#学习笔记
树的面试题解法，一般都是递归：
1. 节点定义；
2. 重复性（自相似性）

递归：
1. 本质是循环
2. 通过函数体来进行的循环

注意点：
1. 抵制人肉递归
2. 找最近重复性
3. 数学归纳法

#每日一题
1、验证二叉搜索树
```
 public boolean isValidBST(TreeNode root) {
        return isValidBST(root, null, null);
    }

    private boolean isValidBST(TreeNode node, Integer min, Integer max) {
        if (node == null) {
            return true;
        }

        if (min != null && node.val <= min) {
            return false;
        }

        if (max != null && node.val >= max) {
            return false;
        }

        return isValidBST(node.left, min, node.val) && isValidBST(node.right, node.val, max);
    }
```
2.最长公共前缀  
反向思维，把字符串a与当前的str匹配，若str中不包含以a这个前缀，则不断减少a的长度，直到str中包含a这个前缀为止。

**注意：**

1.当a为""时，说明无公共前缀，可以直接返回。

2.`str.startsWith(a)`，若str以a为前缀，则返回true，否找返回false.
```
class Solution {
    public String longestCommonPrefix(String[] strs) {
        String a = "";
        try {
            a = strs[0];
            for (String str : strs) {
                // 若a已经减为""，则说明无公共前缀，直接返回
                if (a == "") return a;
                // 若a在当前str中匹配不上，则减少字符串a的长度，再次尝试匹配
                while (!str.startsWith(a)) {
                    a = a.substring(0,a.length() - 1);
                }
            }
            return a;
        } catch (Exception e) {
            return a;
        }
    }
}
```
3、n皇后问题
```
class Solution {
    List<List<String>> res = new ArrayList<>();
    public List<List<String>> solveNQueens(int n) {
        char[][] board = new char[n][n];
        for (char[] i : board){
            Arrays.fill(i,'.');
        }
        backtrack(board,0);
        return res;
    }
    // 路径：board 中小于 row 的那些行都已经成功放置了皇后
    // 选择列表：第 row 行的所有列都是放置皇后的选择
    // 结束条件：row 超过 board 的最后一行
    void backtrack(char[][] board, int row){
        if (row == board.length){
            res.add(array2List(board));
            return;
        }

        for (int j = 0;j<board.length;j++){
            if (!check(board,row,j)){
                continue;
            }
            board[row][j] = 'Q';
            backtrack(board,row+1);
            board[row][j] = '.';
        }
    }

    List<String> array2List(char[][] board){
        List<String> res = new LinkedList<>();
        for (char[] i : board){
            StringBuffer sb = new StringBuffer();
            for (char j : i){
                sb.append(j);
            }
            res.add(sb.toString());
        }
        return res;
    }

    boolean check(char[][] board,int row,int col){
        int n = board.length;
        // 检查列是否有皇后互相冲突
        for (int i = 0; i < n; i++) {
            if (board[i][col] == 'Q')
                return false;
        }
        // 检查右上方是否有皇后互相冲突
        for (int i = row - 1, j = col + 1;
             i >= 0 && j < n; i--, j++) {
            if (board[i][j] == 'Q')
                return false;
        }
        // 检查左上方是否有皇后互相冲突
        for (int i = row - 1, j = col - 1;
             i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q')
                return false;
        }
        return true;
    }
}
```


