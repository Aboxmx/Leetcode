# LeetCode

leetcode做题心得

## 0.目录

[TOC]



## 1.说明

1. 模板代表当前题目的主体结构需要烂熟于心，作为难题的基本构件使用
2. 每个题目尽量给出自己认为比较好的解法

## 2.总纲

1. 对于递归算法：

   1. 递归流程：

      * 写出当前方法的功能

      * 写出子方法的功能

      * 写出当前方法与子方法的关系

      * 写出关系：减而治之，分而治之

      * 写出递归基

      * 写出返回值
   2. 递归设计策略
      * 宏观角度：
        * 写递归算法，即是在找问题的等价说法，并且这个等价说法还是包含这个问题的子问题，可以直接考虑递归算法的子问题，列出子问题，再寻找与问题的关系 
      * 微观角度：
        * 思考，第一个被销毁的栈，自下而上的完成这个任务


2. 对于遍历的算法：
   * 找到对应的遍历模式
   * 注意每一次枚举一个元素后，该循环必然执行的代码
   * 再特别注意，每次循环，通过条件判断所需执行的代码

3. 对于状态转换的算法：
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

- 双指针之相交链表

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

  - 
  






