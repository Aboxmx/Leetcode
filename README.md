# LeetCode

leetcode做题心得

## 0.目录

[TOC]



## 1.说明

1. 模板代表当前题目的主体结构需要烂熟于心，作为难题的基本构件使用
2. 常识代表CS中常出现一些基础知识
3. 每个题目尽量给出自己认为比较好的解法
4. “在计算机科学中,循环不变性(loop invariant,或“循环不变量”),是一组在循环体内、每次迭代均保持为真的性质,通常被用来证明程式或伪码的正确性(有时但较少情况下用以证明算法的正确性)。简单说来,“循环不变性”是指在循环开始和循环中,每一次迭代时为真的性质。这意味着,一个正确的循环体,在循环结束时“循环不变性”和“循环终止条件”必须同时成立。 由于循环和递归的相通,证明带有不变性的循环的部分正确性和证明通过归纳的递归程序的正确性极其相似。”

## 2.总纲

### 1.递归算法设计

1. 递归流程：

   * 写出当前方法的功能
   * 写出子方法的功能
   * 写出当前方法与子方法的关系：减而治之，分而治之
   * 写出处理过程
   * 写出递归基
   * 若有返回值，则写出返回值
2. 递归设计策略
   * 宏观角度：
     * 写递归算法，即是在找问题的等价说法，并且这个等价说法还是包含这个问题的子问题，可以直接考虑递归算法的子问题，列出子问题，再寻找与问题的关系 
   * 微观角度：
     * 思考，第一个被销毁的栈，自下而上的完成这个任务

### 2.遍历算法设计

* 找到对应的遍历模式
* 注意每一次枚举一个元素后，该循环必然执行的代码
* 再特别注意，每次循环，通过条件判断所需执行的代码

### 3.状态转换算法设计

* 注意循环的时候，是一种转态切换，此时的i没有太多含义，仅仅代表状态变换的次数，与遍历算法不同
* 一般会初始化状态1，所以对于一个求第n状态的程序，仅仅需要循环n-1次
 * 图：1->2->3->4 对于循环，可能循环体更像->,因为这标志着状态有1切换到2

## 3.注意点

1. 对于输入为数组，或字符串这类的引用类型，在处理之前需要进行特判



## 4.模板

### 1.数组模板

- 选取数组的有序二元组，即二元组的第一元素位于元组的第二元素前面

  - ~~~java
    // 输入int[] nums
    
    // 1.特判
    if (nums == null || nums.length == 0) { /* return */ }
    
    // 2.初始化
    int len = nums.length;
    // 3.遍历
    for (int i = 0; i < len - 1; i++) {
    	for (int j = i + 1; j < len; j++) {
            // process
        }
    }
    ~~~

* 双指针之：一者固定变，一者有条件的变

  * ~~~java
    int j = 0;
    for (int i = 0; i < nums.length; i++) {
    	if (condition(nums[i])) {
            // process
            // change j : such as j++
        }
        // process
    }
    ~~~

  * 

### 2.链表模板

- 快慢指针之环形链表

  - ~~~java
    // 输入ListNode head
    
    // 1.特判
    if (head == null || head.next == null) { /* return */}
    
    // 2.初始化
    ListNode slow = head;
    ListNode fast = head;
    
    // 3.遍历 
    /*
     * 退出循环时：
     * 对于偶数个节点 <==> fast指向哨兵节点 , slow指向右中位数节点
     * 对于奇数个节点 <==> fast指向最后一个节点， slow指向中间节点
     */
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) {
            return true;
        }
    }
    
    // 4.返回
    return false;
    
    ~~~

- 双指针之相交链表（齐头并进）

  - ~~~java
    //输入ListNode headA, ListNode headB
    
    // 1.特判
    if (headA == null || headB == null) { /* return */ }
    
    // 2.初始化
    ListNode pA = headA;
    ListNode pB = headB;
    
    // 3.遍历
    while (pA != pB) {
        pA = (pA == null) ? headB : pA.next;
        pB = (pB == null) ? headA : pB.next;
    }
    
    // 4.返回
    return pA;
    ~~~

- 前后指针之反转链表(亦步亦趋)

  - ~~~java
    // 输入ListNode head
    
    // 1.特判
    if (head == null || head.next == null) { return head; }
    
    // 2.初始化
    ListNode pre = null;
    ListNode cur = head;
    
    // 3.遍历
    while (cur != null) {
        ListNode tmp = cur.next;
        cur.next = pre;
        pre = cur;
        cur = tmp;
    }
    
    // 4.返回
    return tmp;
    ~~~



### 3.树模板

* 中序遍历之顺序有关（分析与设计依照这个思路流程来）

  * ~~~java
    ### 思路：
    
    #### 1.宏观：
    
    * 将以root为根的数转换为累加树 <==> 先将以它的右子树转换为累加树，在记录累加值，将根节点的值更新为累加值，在将它的左子树转换为累加树
    
    #### 2.微观：
    
    * 该方法的功能：转换root为根的二叉树
    * 子方法的功能：转换root.right为根的二叉树 转换root.left为根的二叉树
    * 关系：先右 处理后 再左
    * 处理：更新累加值， 并用累加值更新当前节点的val
    * 递归基： 若处理空树，则返回null
    * 返回值：返回树根节点
        
    #### 3.递归跟踪：采用局部分析
    
    * 先分析叶子结点这一层，再分析叶子结点的上一层
        
    ### 代码
    class Solution {
        private int sum = 0;
        //该方法的功能：转换root为根的二叉树
        public TreeNode convertBST(TreeNode root) {
            //递归基
            if (root == null) {
                return root;
            }
    
    
            //子方法的功能：装换root.right为根的二叉树
            convertBST(root.right);
    
             //处理
            sum += root.val;
            root.val = sum;
    
            //子方法的功能：装换root.left为根的二叉树
            convertBST(root.left);
            
            return root;
        }
    }
    ~~~

* 后续遍历之顺序无关（分治）

  * ~~~java
    ### 思路：
        
    #### 1.宏观：
    
    * 反转以root为根的二叉树 <==> 反转以它的左子树 ，反转它的左子树树，最终将这两颗翻转后的二叉树交换顺序连接到root中
    
    #### 2.微观：
    
    * 该方法的功能：翻转以root为根的二叉树
    * 子方法的功能：翻转root.left为根的二叉树 翻转root.right为根的二叉树
    * 关系：分治，先翻转左子树或右子树不影响结果
    * 处理：将翻转后的左子树插入到根的右引用，右子树插入到根的左引用
    * 递归基：若处理空树，则返回null
    * 返回值：返回树根节点
    
    #### 3.递归跟踪：采用局部分析
    
    * 先分析叶子结点（此时两次方法调用均会到达递归基）这一层，再分析叶子结点的上一层
        
    ###  代码：
    class Solution {
        public TreeNode invertTree(TreeNode root) {
            if (root == null) {
                return null;
            }
            TreeNode l = invertTree(root.left);
            TreeNode r = invertTree(root.right);
            root.left = r;
            root.right = l;
            return root;
        }
     
    }
    ~~~

  * 









## 6.常识

### 1.汉明距离

* 汉明距离是使用在数据传输差错控制编码里面的，汉明距离是一个概念，它表示两个（相同长度）字对应位不同的数量，我们以d（x,y）表示两个字x,y之间的汉明距离。对两个字符串进行异或运算，并统计结果为1的个数，那么这个数就是汉明距离。

* ~~~java
  // 先对两个数字进行异或操作，然后统计结果中1的个数
  // x & x-1 将会使x的二进制最右边的1变为0
  class Solution {
      public int hammingDistance(int x, int y) {
          int res = x ^ y;
          int count = 0;
          while (res != 0) {
              res &= (res - 1);
              count++;
          }
          return count;
      }
  }
  ~~~

* 
